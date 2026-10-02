# Modera for Muse

**Bringing wardrobe organization and outfit selection into a conversation.**

[Back to showcase](../README.md) · [Product and installation guide](https://www.modera.fyi/muse)

## The opportunity

The iPhone app offers a visual interface for managing a wardrobe. Muse creates another entry point: a person can bring photos or permitted clothing receipts into a conversation, build a wardrobe, and ask what to wear without installing the iPhone app.

The integration needed to do more than return an outfit in text. It needed to preserve wardrobe records, distinguish actual clothing from generated illustrations, request appropriate permissions, and display results that refer back to the right items.

## My contribution

I built the local wardrobe tools, protected service connection, metadata-only outfit API, and shared Swift outfit engine integration. I also implemented package verification and compatible updates, with checks designed to preserve existing wardrobe records and authorization.

## The experience

1. **Connect with permission.** Follow the public installation guide and authorize outfit requests through Muse's protected connection flow.
2. **Build a wardrobe inside Muse.** Use uploads or available, permitted sources. Optional clothing-receipt import uses Muse's Gmail access when authorized.
3. **Ask for an outfit.** Send selected garment facts to Modera's outfit service and receive combinations tied to those items.
4. **Inspect the result.** Display the selected pieces as a panel or an assembled look, and support saving a chosen outfit in the Muse wardrobe.

<p align="center">
  <img src="../assets/muse/panel-view.jpg" alt="Two fictional sample outfits displayed in Muse as garment panels." width="285">
  &nbsp;
  <img src="../assets/muse/assembled-view.jpg" alt="The same sample outfits shown as assembled looks on invisible mannequins." width="285">
</p>

*Sample wardrobes · AI-generated garment imagery. Modera selected the combinations; Muse generated the visual appearances. These are product demonstrations, not personal wardrobe records.*

## Decisions and tradeoffs

| Decision | What it accomplishes |
| :--- | :--- |
| Keep the wardrobe inside Muse | Modera's service does not need to receive photos, garment images, conversations, or saved outfits. Muse remains a hosted service with its own data practices. |
| Share the outfit engine across environments | Preserve the core styling behavior while adapting product-specific constraints for a conversational workflow. |
| Separate garment facts from generated imagery | A plausible-looking illustration does not establish what a person owns or what a garment actually looks like. |
| Explain when no outfit can be produced | Return useful information about missing inputs or incompatible combinations instead of leaving the user at a dead end. |
| Distinguish missing additions from owned pieces | A proposed purchase should not silently become part of a ready-to-wear outfit or the user's wardrobe. |
| Verify updates before applying them | Check package integrity and compatibility while preserving wardrobe records and protected credentials. |

## Engineering

Python and Pillow support the wardrobe tools in Muse. A TypeScript/Node.js API on Google Cloud Run invokes the Swift outfit engine. The connection uses OAuth with PKCE, credential rotation, and revocation. Requests project a selected set of clothing facts across the service boundary. Results reference request-scoped garment aliases that Muse maps back to local items.

Images are handled using Muse's native hosted image capabilities. “Inside Muse” does not mean offline or on-device processing. The iPhone app's wardrobe is separate; this connector does not provide automatic app-to-Muse wardrobe synchronization.

## Delivery and evidence

A public guided-installation flow and limited outfit API access are available through the linked product page. The installation tools and instructions are inspectable; proprietary outfit rules stay on the server.

The project includes automated checks for request validation, package integrity, updates, and record preservation. Existing demonstrations establish outfit generation and display. They do not establish every source integration, every fresh-account onboarding path, or end-to-end acceptance of every later release. Source access also depends on Muse's available capabilities and the user's permissions.

[Explore the architecture →](architecture.md)
