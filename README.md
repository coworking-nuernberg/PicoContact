# PicoContact

Fork of [nliautaud/p01contact](https://github.com/nliautaud/p01contact) — a simple contact form plugin for [Pico CMS](http://picocms.org).

## Fork changes

This fork adds **Cloudflare Turnstile** as an alternative captcha provider alongside the existing Google reCAPTCHA v2 support.

### Why Turnstile?

- **Free** — no usage limits
- **Privacy-friendly** — no tracking cookies, GDPR-friendly
- **Less intrusive** — often invisible to users (no "click all traffic lights")
- **Same verify API format** as reCAPTCHA — minimal code change

### Configuration

In `config.json`, add:

```json
{
    "captcha_provider": "turnstile",
    "recaptcha_public_key": "<your-turnstile-site-key>",
    "recaptcha_secret_key": "<your-turnstile-secret-key>",
    "turnstile_appearance": "interaction-only"
}
```

| Setting | Values | Default | Description |
|---------|--------|---------|-------------|
| `captcha_provider` | `recaptcha`, `turnstile` | `recaptcha` | Which captcha service to use |
| `recaptcha_public_key` | string | *(empty)* | Site key (reCAPTCHA or Turnstile) |
| `recaptcha_secret_key` | string | *(empty)* | Secret key (reCAPTCHA or Turnstile) |
| `turnstile_appearance` | `always`, `interaction-only`, `execute` | `interaction-only` | Widget visibility (Turnstile only) |

**Appearance modes:**
- `always` — widget always visible
- `interaction-only` — only visible when Cloudflare needs user interaction
- `execute` — completely invisible, runs in background

### Form syntax

Add `captcha` to your form definition:

```
(% contact en :
    name!,
    email!,
    message!,
    captcha,
%)
```

### Backwards compatibility

Existing reCAPTCHA setups continue to work without changes. Without `captcha_provider` in config.json, the plugin defaults to Google reCAPTCHA.

## Original features

- Supports any field types
- Powerful [textual syntax](https://github.com/nliautaud/p01contact/wiki/Syntax)
- Generates [comprehensive mails](https://github.com/nliautaud/p01contact/wiki/Emails)
- UTF-8, [localized and multilingual](https://github.com/nliautaud/p01contact/wiki/Localization-(i18n))
- Automatic [security measures](https://github.com/nliautaud/p01contact/wiki/Settings#security) (honeypot, timing, rate limiting)
- Plugin for GetSimple or Pico CMS

## Installation

For [Pico CMS](http://picocms.org), place the `p01-contact` directory in `plugins/` and rename it to `PicoContact`.

*Compatibility: PHP 5.4+*

## License

[MIT](LICENSE) — original by [Nicolas Liautaud](https://github.com/nliautaud)
