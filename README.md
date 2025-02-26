# Prestashop Cloudflare Turnstile

[![Minimum PHP Version](https://img.shields.io/badge/php-%3E%3D%207.2-green)](https://php.net/)
[![Minimum Prestashop Version](https://img.shields.io/badge/prestashop-%3E%3D%201.7.6.0-green)](https://www.prestashop.com)
[![GitHub release](https://img.shields.io/github/v/release/Pixel-Open/prestashop-cloudflare-turnstile)](https://github.com/Pixel-Open/prestashop-cloudflare-turnstile/releases)

## Presentation

[Turnstile](https://developers.cloudflare.com/turnstile/) is Cloudflare's smart CAPTCHA alternative. The module allows Turnstile to protect your Prestashop forms:

- Contact
- Login
- Register
- Reset password
- Checkout Login
- Checkout Register

![Cloudflare Turnstile](screenshot.png)

**Note:** Activating a Captcha in the checkout can alter the user experience. A "stupid" bot will rarely reach this stage (cart requirement). To be activated only if necessary.

## Requirements

- Prestashop >= 1.7.6.0
- PHP >= 7.2.0

## Installation

Download the **pixel_cloudflare_turnstile.zip** file from the [last release](https://github.com/Pixel-Open/prestashop-cloudflare-turnstile/releases/latest) assets.

### Admin

Go to the admin module catalog section and click **Upload a module**. Select the downloaded zip file.

### Manually

Move the downloaded file in the Prestashop **modules** directory and unzip the archive. Go to the admin module catalog section and search for "Cloudflare Turnstile".

## Configuration

- **Sitekey**: the sitekey given for the site in your Cloudflare dashboard
- **Secret key**: the secret key given for the site in your Cloudflare dashboard
- **Theme**: the Turnstile theme (auto, light or dark)
- **Forms to validate**: the forms where a Turnstile validation is required

For the registration form, the widget is automatically added with a hook. For "contact", "login" and "reset password" forms, **you need to manually add the widget in the template files**, usually before the validation button.

**Never select a form to validate without the widget in the form template.**

## Widget

For contact, login and reset password forms, you need to manually add the widget in the template files.

### Contact

**Template**:

themes/{themeName}/modules/contactform/views/templates/widget/contactform.tpl

**Widget**:

```smarty
{widget name='pixel_cloudflare_turnstile' form='contact'}
```

### Login

**Template**:

themes/{themeName}/templates/customer/_partials/login-form.tpl

**Widget**:

```smarty
{widget name='pixel_cloudflare_turnstile' form='login'}
```

### Reset password
**Template**:
themes/{themeName}/templates/customer/password-email.tpl
**Widget**:
```smarty
{widget name='pixel_cloudflare_turnstile' form='password'}
```

### Custom Form
**Widget**:
```smarty
{widget name='pixel_cloudflare_turnstile' custom='1' action='custom-form'}
```

**Note:** The action param is a free name that will appear in the Turnstile statistics


## Testing

Use the following sitekeys and secret keys for testing purposes:

**Sitekey**

| Sitekey                  | Description                     |
|--------------------------|---------------------------------|
| 1x00000000000000000000AA | Always passes                   |
| 2x00000000000000000000AB | Always blocks                   |
| 3x00000000000000000000FF | Forces an interactive challenge |

**Secret key**

| Secret key                          | Description                          |
|-------------------------------------|--------------------------------------|
| 1x0000000000000000000000000000000AA | Always passes                        |
| 2x0000000000000000000000000000000AA | Always fails                         |
| 3x0000000000000000000000000000000AA | Yields a "token already spent" error |