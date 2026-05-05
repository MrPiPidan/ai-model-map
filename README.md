# AI Model Map

A comprehensive, community-maintained registry of AI model capabilities across all major providers.

一份社区维护的 AI 模型能力配置表，覆盖国内外主流大模型厂商，任何 AI 客户端/工具可直接引用。

## Features

- Thinking/Reasoning capability detection (effort levels, always-on, toggle)
- Multimodal support (vision, audio)
- Function calling & structured output
- Context window sizes
- Provider-specific request parameter mappings
- Regex-based model matching

## Covered Providers

| Provider | Models |
|----------|--------|
| OpenAI | GPT-5.5, GPT-5.x, o-series, GPT-4.x |
| Anthropic | Claude Opus 4.7, Sonnet 4.6, Opus 4.6/4.5, 3.x |
| DeepSeek | V4-Pro, V3.x, R1 |
| Qwen (通义千问) | Qwen3.5/3.6, Qwen3, QwQ, VL, Omni |
| Kimi (月之暗面) | K2 Thinking, K2.5/K2.6 |
| GLM (智谱) | GLM-5.1/5/4.7/4.6/4.5 |
| Doubao (豆包) | Seed 2.0 |
| Hunyuan (腾讯混元) | T1, 2.0-Thinking |
| StepFun (阶跃星辰) | Step-3.5-flash, Step-3 |
| MiMo (小米) | V2.5-Pro, Flash, Omni |
| MiniMax | M2 series |
| xAI | Grok 4.x, Grok 3 Mini |
| Mistral | Magistral, Small/Medium |
| Google | Gemini 3.x, 2.5 |

## Usage

### Direct URL (via jsDelivr CDN)

```
https://cdn.jsdelivr.net/gh/MrPiPidan/ai-model-map@main/model_capabilities.json
```

### In your app

Fetch the JSON, match model IDs against `pattern` (regex), first match wins.

```swift
// Swift example
let cap = rules.first { rule in
    modelId.range(of: rule.pattern, options: .regularExpression) != nil
}
```

```python
# Python example
import re
cap = next((r for r in rules if re.match(r["pattern"], model_id)), None)
```

## Schema

Each rule contains:

```json
{
  "pattern": "regex to match model ID",
  "name": "Human-readable name",
  "provider": "provider identifier",
  "capabilities": {
    "thinking": true,
    "thinking_always_on": false,
    "vision": true,
    "audio": false,
    "function_calling": true,
    "structured_output": true
  },
  "context": { "max_input": 1000000, "max_output": 128000 },
  "efforts": ["low", "medium", "high", "max"],
  "thinking_config": {
    "param": { "type": "adaptive" },
    "effort_param_name": "effort",
    "effort_location": "output_config",
    "disallow_sampling_when_thinking": true,
    "response_field": "reasoning_content"
  }
}
```

## Contributing

PRs welcome! When adding a new model:

1. Add a new rule entry **above** the fallback `".*"` rule
2. Increment the `version` field
3. Update the `updated` date
4. Include the official documentation link as `_source`

## License

MIT
