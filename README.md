# Z Image Turbo Prompts — 8 Tested Recipes With Outputs

<!-- conv-kit:v1 -->

<p align="center">
  <img src="assets/badges/price.svg" alt="observed unit price"> <img src="assets/badges/billing.svg" alt="billing model"> <img src="assets/badges/compat.svg" alt="OpenAI-compatible endpoint">
</p>

<p align="center">
  <img src="assets/01-product-hero-perfume.jpg" width="820" alt="Sample render via the APIMart image API">
</p>

> **from $0.01 per image** on the APIMart route — `https://api.apimart.ai/v1` の OpenAI 互換エンドポイント1つだけ、月額プランは不要です。*(2026-10-12 時点)*

**[Get an API key](https://go.apimart.ai/k-4f5603)** · **[Live pricing](https://go.apimart.ai/k-e4e2d5)** · **[Model page](https://go.apimart.ai/k-f987aa)** · [⚡ 60-second quickstart](#quickstart)

**チームが APIMart 経由で Z Image Turbo（`z-image-turbo`）を使う理由**

- **キー1つでカタログ全体。**同じ `https://api.apimart.ai/v1` の base URL と `Authorization` ヘッダーで Z Image Turbo（`z-image-turbo`）と画像・動画・言語モデルなど 300+ のモデルにアクセスできます。切り替えるのは `model` フィールドだけで、クライアント側の変更は不要です。
- **最低 $1 から、従量課金。**サブスクリプションも、事前に規模を見積もるプリペイドプランもありません。$1 からチャージして、呼び出した分だけ使えます。
- **課金内容はレスポンスで返ります。**完了したタスクはすべて請求額（`cost` / `credits_cost`）を報告し、`failed` になったタスクは返金されます。
- **非同期前提の設計。**送信して `task_id` を受け取り、`GET /v1/tasks/{id}` をポーリングするだけ。バッチ処理もリトライも特別な統合ではなく、普通のキュー処理です。

<!-- /conv-kit:v1 -->



Eight **Z Image Turbo prompts** listed with an example render, the ratio, and what the call costs on this route. Copy a recipe, keep the structure, swap the subject.

- Model: `z-image-turbo`
- Recipes: **8** (machine-readable in [`data/prompts.json`](data/prompts.json), table in [`PROMPTS.md`](PROMPTS.md))
- Effective price used below: **$0.01 per image** — estimated cost of the whole set: **$0.08**

## What separates a usable recipe from a wasted call

Three rules held up across every render in this set:

1. **Name the material, not the adjective.** "Frosted glass", "matte ceramic", "layered paper" steer rendering far more
   than "beautiful" or "high quality".
2. **Set the light explicitly.** "Single softbox from the left", "golden hour backlight", "focus-stacked studio light"
   remove the guesswork the model would otherwise do for you.
3. **Pin the framing.** Ratio plus lens language (`85mm`, `24mm`, `macro`, overhead flat lay) decides whether the output
   drops into a layout unchanged.

## Prompt structure cheat-sheet

| Slot | What to write | Example |
| --- | --- | --- |
| Subject | one concrete object or person, with material | *frosted glass perfume bottle* |
| Light | direction + quality | *single softbox from the left* |
| Framing | ratio + lens or distance | *3:4, medium format look* |
| Setting | surface, backdrop, environment | *wet black stone slab* |
| Finish | render or film character | *commercial product photography* |

## The gallery

Each row is one recipe: example render, category, ratio, cost on this route and the exact prompt.

| Output | Recipe | Ratio | Cost | Prompt |
| --- | --- | --- | --- | --- |
| <img src="assets/01-product-hero-perfume.jpg" width="220" alt="Sample render via the APIMart image API"> | Product / e-commerce | 1:1 | $0.01 | `Studio hero shot of a frosted glass perfume bottle on a wet black stone slab, single softbox from the left, faint mist, deep charcoal background, crisp label text, commercial product photography` |
| <img src="assets/02-food-overhead-ramen.jpg" width="220" alt="Sample render via the APIMart image API"> | Food photography | 4:3 | $0.01 | `Overhead flat lay of a spicy miso ramen bowl with soft boiled egg, nori and scallions, dark ceramic table, chopsticks resting on the rim, natural window light, editorial food photography` |
| <img src="assets/03-cinematic-street-rain.jpg" width="220" alt="Sample render via the APIMart image API"> | Cinematic still | 16:9 | $0.01 | `Rain soaked Kyoto alley at night, paper lantern reflections on wet stone, a lone figure with a transparent umbrella walking away, cinematic 35mm still, shallow depth of field, film grain` |
| <img src="assets/04-architectural-dusk.jpg" width="220" alt="Sample render via the APIMart image API"> | Architecture | 16:9 | $0.01 | `Minimalist concrete villa on a cliff at dusk, warm interior light, infinity pool reflecting a violet sky, architectural photography, 24mm perspective, ultra sharp` |
| <img src="assets/05-fashion-editorial-studio.jpg" width="220" alt="Sample render via the APIMart image API"> | Fashion portrait | 3:4 | $0.01 | `Editorial fashion portrait of a model in an oversized ivory wool coat, seamless light grey studio backdrop, crisp high key lighting, medium format detail, calm expression` |
| <img src="assets/06-illustration-layered-paper.jpg" width="220" alt="Sample render via the APIMart image API"> | Illustration | 1:1 | $0.01 | `Layered paper cut illustration of a mountain lake at sunrise, five depth layers, soft pastel palette, subtle drop shadows, art print composition, clean vector edges` |
| <img src="assets/07-infographic-dashboard.jpg" width="220" alt="Sample render via the APIMart image API"> | Design / UI | 16:9 | $0.01 | `Flat vector dashboard panel showing three gauge dials and abstract latency curves, muted blue and sand palette, generous white space, crisp geometric cards, no placeholder text` |
| <img src="assets/08-macro-botanical-detail.jpg" width="220" alt="Sample render via the APIMart image API"> | Macro nature | 3:2 | $0.01 | `Macro photograph of a dew covered dandelion seed head against deep black background, focus stacked detail, iridescent droplets, studio lighting` |

## Run a recipe yourself

```bash
export APIMART_API_KEY=...
python examples/run_recipes.py --dry-run                 # list the recipes, no network
python examples/run_recipes.py --limit 2                 # generate two of them
```

```bash
curl --request POST --url https://api.apimart.ai/v1/images/generations \
  --header "Authorization: Bearer $APIMART_API_KEY" --header 'Content-Type: application/json' \
  -d '{"model":"z-image-turbo","prompt":"<paste a prompt>","size":"1:1","resolution":"1K"}'
```

Result links expire 72 hours after completion, so store the outputs; the completed task carries `cost` for reconciliation.

## FAQ

**Are these prompts free to reuse?**

Yes — the prompt text in this repository is MIT licensed. The generated images and any third-party marks they contain remain your responsibility, and you should check the model vendor's terms before publishing commercial work.

**Why do the recipes use different aspect ratios?**

Because ratio is a layout decision, not a style one: 1:1 for catalogue and icons, 16:9 for hero and video thumbnails, 3:4 or 2:3 for portraits and print. Pinning it up front avoids cropping later.

**How much does one recipe cost to run?**

**from $0.01 per image** on the APIMart route. Every completed task reports the exact amount in its `cost` field; a failed task is refunded.

**Can I use a recipe as a template for another subject?**

That is the point. Keep the structure (subject + light + framing + setting + finish) and replace the subject; changing everything at once makes it impossible to tell which phrase moved the output.

<!-- related-repos:auto -->
## Related repositories

- **Same model, this language** — the other half of this pair: [z-image-api-ja](https://github.com/ej094tn/z-image-api-ja)
- **Same model, other languages** — 9 more language builds: 中文 [z-image-api-cn](https://github.com/vbu-o4gm/z-image-api-cn) · Deutsch [z-image-api-de](https://github.com/e378pu80/z-image-api-de) · Español [z-image-api-es](https://github.com/r91kz/z-image-api-es) · Français [z-image-api-fr](https://github.com/qxhjep3w5me/z-image-api-fr) · Relay/gateway `z-image-api-gateway` · Bahasa [z-image-api-id](https://github.com/x5qdsi/z-image-api-id) · 한국어 [z-image-api-ko](https://github.com/x69ynmals73l4z/z-image-api-ko) · Português `z-image-api-pt` · Русский [z-image-api-ru](https://github.com/zndjw/z-image-api-ru)
- **More models in this language** — [midjourney-api-ja](https://github.com/apimartt1q/midjourney-api-ja) · [gemini-2-5-flash-image-preview-api-ja](https://github.com/ic7skkh/gemini-2-5-flash-image-preview-api-ja) · [nano-banana-api-ja](https://github.com/e4ylndl3g-v/nano-banana-api-ja) · [gemini-3-1-flash-image-preview-api-ja](https://github.com/gv4ju/gemini-3-1-flash-image-preview-api-ja) · [nano-banana-2-api-ja](https://github.com/lpbxkrzbfel/nano-banana-2-api-ja) · [gemini-3-pro-image-preview-api-ja](https://github.com/zzsxs8r/gemini-3-pro-image-preview-api-ja)
- **Topic hubs** — every build of this model, all languages: [z-image](https://github.com/topics/z-image) · [z-image-api](https://github.com/topics/z-image-api)

This repository is one build in a cross-linked set of API guides for the same model family; each language build links back to the others.
<!-- /related-repos:auto -->

## Attributed links (how this repository is measured)

| Purpose | Attributed link | Target |
| --- | --- | --- |
| Model page | <https://go.apimart.ai/k-f987aa> | `apimart.ai/ja/model/z-image-turbo` |
| Live pricing | <https://go.apimart.ai/k-e4e2d5> | `apimart.ai/ja/pricing` |
| Get an API key | <https://go.apimart.ai/k-4f5603> | `apimart.ai/ja/keys` |

Outbound APIMart links are minted through the promo link API; hand-made tracking parameters are rejected by
`tools/check_links.py` in CI.

## Disclosure

Z Image Turbo is a third-party model served through APIMart. This repository publishes prompts, example renders and
cost logic; it does not claim official status for any vendor, and model names and documentation belong to their owners.

## Repository map

```text
README.md              gallery, prompt structure and FAQ
PROMPTS.md             every recipe in one table
data/prompts.json      machine-readable recipes with per-unit cost
examples/run_recipes.py  batch runner (dry-run safe for CI)
tools/check_links.py   attribution guard
assets/                example renders via the APIMart image API (JPEG)
```

## License

MIT — see [LICENSE](LICENSE).
