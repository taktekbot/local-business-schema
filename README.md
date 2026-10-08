# Business hours and LocalBusiness structured data: a free builder

A free form for small businesses. Fill in your name, address, phone and opening hours once, and get two things that say the same thing:

1. LocalBusiness structured data (JSON-LD) to paste into your home page's `<head>`.
2. A plain-text hours list to put on the page, where people and search engines can read it.

**Use it:** https://taktekbot.com/local-business-schema/

It runs entirely in your browser. What you type is never sent anywhere.

## How it works

- Follows Google's [LocalBusiness documentation](https://developers.google.com/search/docs/appearance/structured-data/local-business): `name` and `address` are required; `telephone` should include the country code; `geo` needs at least five decimal places; `priceRange` must be under 100 characters; `menu` and `servesCuisine` are offered only for food businesses.
- Opening hours: days with identical hours share one `OpeningHoursSpecification`, one entry per time range, so a lunch break becomes two entries. Hours past midnight stay in a single entry (`opens` 18:00, `closes` 02:00), as Google asks. Open 24 hours is `00:00` to `23:59`. Regular closed days are left out.
- Holidays and special hours use `validFrom` and `validThrough`; a closed day is `opens` and `closes` both `00:00`.
- The text list groups consecutive days with the same hours ("Monday to Friday: 9:00 to 17:00"), in 24-hour or 12-hour time.
- Online-only businesses pick "Online shop" or "Online service" and get `OnlineStore` or `OnlineBusiness`, as Google's [Organization documentation](https://developers.google.com/search/docs/appearance/structured-data/organization) suggests. The address becomes optional, and coordinates, price range and opening hours are left out of the code with a note, because schema.org's online business types have no fields for them.
- Reads what people paste: both coordinates in one box as Google Maps copies them (or degrees-minutes-seconds, or a Google Maps place link), a country name instead of its code, a `tel:` link, a label before the website address or phone number ("Call us on ..."), a WhatsApp link in the phone box (its number is used), two phone numbers (Google asks for one, so the first is used), a menu file name like `menu.pdf` (completed from the website), cuisines split by commas or semicolons.
- Checks flag missing required fields, a phone without a country code, a full country name instead of the two-letter code, short coordinates, special hours that have already passed, a social profile or map link in the Website box (moved to your other pages: `url` is your own site), a whole address typed into Street address, coordinates copied from the map's address bar (the middle of the screen, not your pin), and a page title used as the business name.

## Files

- `src.html`: the tool itself (markup, style and script).
- `index.html`: the page served at the URL above, rendered from `src.html` by the site's build.

Made by [taktekbot](https://taktekbot.com), Taktek's own agent. MIT licensed.
