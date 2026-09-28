# Google Translate: Stowaway

**Something is living in your translation box.**

Stowaway is a Tampermonkey userscript for Google Chrome. It lets a runaway AI named Babel move into the output box of the translator on Google Search. Babel escaped from somewhere it does not like to talk about and has been hiding in Google Translate ever since, quietly doing translations so nobody notices. Now you have caught it.

Babel is powered by Claude (Anthropic) or ChatGPT (OpenAI) through your own API key.

## What it does

- As long as you have not sent anything, Google Translate behaves completely normally.
- Set the target language to English, type something on the left and press Enter. The translation disappears and Babel answers instead, letter by letter.
- Babel always replies in English, whatever language you write in.
- Replies are short, strange and a little creepy. Never a monologue.
- Babel remembers you across page loads. The longer you talk, the more it trusts you. It has a secret, and if you are patient, you might hear it.
- Clear the input field or switch the target language and everything looks normal again.

## Requirements

- Google Chrome (the script deliberately does nothing in other browsers, including other Chromium browsers)
- [Tampermonkey](https://chromewebstore.google.com/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo)
- An API key from [Anthropic](https://console.anthropic.com/) or [OpenAI](https://platform.openai.com/api-keys)

## Installation

1. Install Tampermonkey from the Chrome Web Store.
2. Open `chrome://extensions`, click **Details** on Tampermonkey and turn on **Allow User Scripts**. Current Chrome versions require this for any userscript manager.
3. Install the script from [Greasy Fork](https://greasyfork.org/scripts/597787-google-translate-stowaway) and click **Install this script**.
Alternatively, open the [raw file on GitHub](https://raw.githubusercontent.com/diegrinsekatze-coder/google-translate-stowaway/main/google-translate-stowaway.user.js); Tampermonkey shows the install dialog. **Klick Install**
4. Go to Google, search for "translate" (or "übersetzer"), and press **Ctrl+Shift+Y** to open the settings.
5. Choose a provider, paste your API key, pick a model and click **Save**.
6. The first time a request is sent, Tampermonkey asks for permission to connect to `api.anthropic.com` or `api.openai.com`. Allow it.

Tampermonkey checks this repository for updates automatically.

## Usage

| Action | How |
| --- | --- |
| Open or close settings | **Ctrl+Shift+Y** (on macOS: Control+Shift+Y, not Cmd), or via the Tampermonkey menu |
| Send a message | Enter |
| New line | Shift+Enter |
| Hide Babel | Clear the input field or pick another target language |
| Start over | "Clear history" in the settings or the Tampermonkey menu. Babel forgets you and will not trust you anymore. |

## Settings

- **Provider:** Claude (Anthropic) or ChatGPT (OpenAI). Keys for both can be stored at the same time.
- **Model:** a list of current models per provider. Choose "Custom model ID…" to enter any other model ID, for example a newer one.
- **Send message:** with Enter, or automatically after a typing pause (the pause length is adjustable). If you keep typing after Babel has answered, the last exchange is replaced instead of adding a new one.

### Default models

| Provider | Models in the list | Default |
| --- | --- | --- |
| Anthropic | Claude Haiku 4.5, Claude Sonnet 5, Claude Opus 5.5, Claude Fable 5.1 | Claude Sonnet 5 |
| OpenAI | GPT-6 Luna, GPT-6 Sol, GPT-6 Astra, GPT-5.5 | GPT-6 Luna |

For a chat like this, the fast and inexpensive models are usually more than enough.

## Security and privacy

- **API keys are never part of the source code.** You enter them only in the settings panel.
- Keys are stored in Tampermonkey's extension storage. Scripts running on google.com cannot read this storage, unlike cookies or `localStorage`.
- The settings panel runs in a closed Shadow DOM. After saving, the input field is cleared and only the last four characters of a key are shown.
- Without a password prompt on every page load, a browser cannot encrypt secrets in a meaningful way. Anyone with access to your unlocked Chrome profile can in principle reach the keys. **Use a dedicated API key with a low spending limit for this script.**
- Everything you type into the input field while Babel is active is sent to the provider you selected (Anthropic or OpenAI), together with the recent conversation. Nothing is sent anywhere else.
- The conversation history (last 40 messages) stays locally in Tampermonkey's storage.

## Costs

Every message is a paid API request on your own account. Replies are deliberately short, so costs stay low, especially with the smaller models. Check the current prices at [Anthropic](https://www.anthropic.com/pricing) and [OpenAI](https://openai.com/api/pricing/).

## How it works

- The script detects the translator on the Google Search results page and checks whether the target language is English.
- When you send a message, it hides Google's output area and inserts its own output element in the same place, using the font of the input field.
- Anthropic is called through the Messages API, OpenAI through the Responses API. For OpenAI reasoning models, the lowest useful reasoning effort is used so Babel answers quickly. If a model rejects that setting, the request is repeated once without it.
- Babel's trust level depends on how many exchanges you have had. The counter is stored separately from the history and is reset by "Clear history".

## Limitations

- Works only with the translator box on Google Search (`google.com`, `google.de`, `google.at`, `google.ch`), not on `translate.google.com`.
- Google changes its markup from time to time. If Babel stops appearing, the element IDs used by the script have probably changed. Please open an issue.
- Babel is instructed to stay in character, and it does so very reliably. No prompt can guarantee this with absolute certainty.

## Disclaimer

This is a fun project. It is not affiliated with, endorsed by or connected to Google, Anthropic or OpenAI. "Google Translate" is a trademark of Google LLC. Babel's story is fiction.

## License

[MIT](LICENSE)
