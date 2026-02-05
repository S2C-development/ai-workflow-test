# Tool Dependencies Design

## Huidige Situatie

Het project bevat momenteel **geen bestaande tool dependency implementatie**. Dit is een nieuw project met alleen een basis calculator setup in `src/index.ts`.

Er is geen:
- `Tools/` folder
- Bestaande tool implementaties
- Hardcoded dependencies tussen tools

## Voorstel: Configureerbaar Tool Dependency Systeem

### 1. Appsettings.json Structuur

```json
{
  "ToolDependencies": {
    "Git": {
      "requires": [],
      "mandatory": true,
      "description": "Version control tool"
    },
    "Docker": {
      "requires": ["Git"],
      "mandatory": false,
      "description": "Container runtime"
    },
    "Kubernetes": {
      "requires": ["Docker"],
      "mandatory": false,
      "description": "Container orchestration"
    },
    "Terraform": {
      "requires": ["Git"],
      "mandatory": false,
      "description": "Infrastructure as Code"
    },
    "Ansible": {
      "requires": ["Git"],
      "mandatory": false,
      "description": "Configuration management"
    }
  },
  "ToolValidation": {
    "checkOnStartup": true,
    "blockOnMissingMandatory": true,
    "warnOnMissingOptional": true
  }
}
```

### 2. Te Implementeren Files

#### Nieuwe Files:
- `src/tools/ToolRegistry.ts` - Centraal register voor alle tools
- `src/tools/ToolValidator.ts` - Valideert dependencies
- `src/tools/BaseTool.ts` - Abstract base class voor tools
- `src/config/appsettings.json` - Configuratie file
- `src/config/ConfigLoader.ts` - Laadt en parsed configuratie

#### Voorbeeld Tool Implementatie:
- `src/tools/GitTool.ts`
- `src/tools/DockerTool.ts`

### 3. Implementatie Aanpak (KISS)

#### Stap 1: Config Structuur
```typescript
// src/config/ToolConfig.ts
export interface ToolDependencyConfig {
  requires: string[];
  mandatory: boolean;
  description: string;
}

export interface ToolDependencies {
  [toolName: string]: ToolDependencyConfig;
}

export interface AppSettings {
  ToolDependencies: ToolDependencies;
  ToolValidation: {
    checkOnStartup: boolean;
    blockOnMissingMandatory: boolean;
    warnOnMissingOptional: boolean;
  };
}
```

#### Stap 2: Config Loader
```typescript
// src/config/ConfigLoader.ts
import * as fs from 'fs';
import { AppSettings } from './ToolConfig';

export class ConfigLoader {
  static load(path: string = './appsettings.json'): AppSettings {
    const data = fs.readFileSync(path, 'utf-8');
    return JSON.parse(data) as AppSettings;
  }
}
```

#### Stap 3: Tool Validator
```typescript
// src/tools/ToolValidator.ts
export class ToolValidator {
  constructor(private config: ToolDependencies) {}

  validate(toolName: string, availableTools: Set<string>): ValidationResult {
    const toolConfig = this.config[toolName];
    if (!toolConfig) return { valid: false, missing: [], reason: 'Unknown tool' };

    const missing = toolConfig.requires.filter(dep => !availableTools.has(dep));

    return {
      valid: missing.length === 0,
      missing: missing,
      mandatory: toolConfig.mandatory
    };
  }

  validateAll(availableTools: Set<string>): Map<string, ValidationResult> {
    // Valideer alle tools en return resultaten
  }
}
```

#### Stap 4: Tool Registry
```typescript
// src/tools/ToolRegistry.ts
export class ToolRegistry {
  private tools = new Map<string, BaseTool>();
  private validator: ToolValidator;

  register(tool: BaseTool): void {
    const validation = this.validator.validate(
      tool.name,
      new Set(this.tools.keys())
    );

    if (!validation.valid && validation.mandatory) {
      throw new Error(`Cannot register ${tool.name}: missing ${validation.missing}`);
    }

    this.tools.set(tool.name, tool);
  }

  get(name: string): BaseTool | undefined {
    return this.tools.get(name);
  }
}
```

### 4. Gebruik Voorbeeld

```typescript
// src/index.ts
import { ConfigLoader } from './config/ConfigLoader';
import { ToolRegistry } from './tools/ToolRegistry';
import { ToolValidator } from './tools/ToolValidator';

const config = ConfigLoader.load();
const validator = new ToolValidator(config.ToolDependencies);
const registry = new ToolRegistry(validator);

// Registreer tools
registry.register(new GitTool());
registry.register(new DockerTool()); // Vereist Git
```

### 5. Voordelen van Deze Aanpak

1. **Simpel**: Dependency configuratie in één JSON file
2. **Flexibel**: Nieuwe tools toevoegen zonder code changes
3. **Validatie**: Automatisch checken van dependencies bij startup
4. **Duidelijk**: Elke tool declareert explicit wat het nodig heeft
5. **Onderhoudbaar**: Scheiding tussen configuratie en logica

### 6. Testing Strategie

- Unit tests voor ToolValidator met verschillende dependency scenarios
- Integration tests voor ToolRegistry met mock tools
- Config validation tests voor appsettings.json schema

### 7. Migration Pad

Voor bestaande projecten met hardcoded dependencies:
1. Inventariseer alle huidige tool dependencies
2. Migreer naar appsettings.json formaat
3. Vervang hardcoded checks door ToolValidator calls
4. Test met backwards compatibility

## Conclusie

Dit design biedt een **straightforward oplossing** zonder over-engineering:
- Configuratie via JSON (geen complex DSL)
- Simpele validator logica (geen dependency resolution graphs)
- Duidelijke interfaces (geen magic)
- Eenvoudig uit te breiden (nieuwe tools = nieuwe JSON entry)

De implementatie volgt het **KISS principe**: alleen wat nodig is voor configureerbare tool dependencies, niets meer.
