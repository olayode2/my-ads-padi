# My Ads Padi

Front end for the My Ads Padi AI Ads Agent. One static file (`index.html`), no build step, logo embedded.

## Deploy
1. Push `index.html` and this README to a GitHub repo.
2. Vercel: Add New Project, import the repo, framework preset "Other", Deploy.

## Business ID
Open the gear icon at the bottom of the sidebar to set the Business ID and name, or pass them in the link:
`https://your-site.vercel.app/?client_id=abc123&name=Skin%20by%20Ferry`
BOS passes the real client_id the same way when it embeds the page.

## Service endpoints
The page only talks to the n8n webhooks listed in the `API` object at the top of the script in `index.html`. Each entry has a `live` flag. Features whose workflow is not published yet show "This feature is being connected" when used. Flip the flag to `true` when the workflow goes live.

| Feature | Path | Live |
|---|---|---|
| New Campaign, steps 1 and 2 | `/ads-padi/campaign/save` | yes |
| New Campaign, step 3 write offers | `/ads-padi/offers/generate` | yes |
| New Campaign, step 3 pick offer | `/ads-padi/offers/select` | yes |
| New Campaign, step 4 generate | `/ads-padi/campaign/generate` | not yet |
| Campaign Research, list past campaigns | `/ads-padi/campaign/list` | not yet (browser cache until then) |
| AI Videos, make video from the campaign script | `/ads-padi/video/generate` | not yet |
| AI Videos, check a rendering video | `/ads-padi/video/status` | not yet |
| AI Graphics, flyer from the campaign flyer copy | `/ads-padi/graphics/design` | not yet |
| Landing Pages build and revise | `/ads-padi/landing/build` | not yet |
| Landing Pages publish | `/ads-padi/landing/publish` | not yet |
| Brand Assets | `/ads-padi/brand/upload` | not yet |

Request and response shapes are in the comments next to each path. Campaigns, offers, copy, media and assets are also cached in the browser per Business ID so the page remembers where the owner stopped.

## Screens
- Campaign Research: every campaign the business has run, searchable; open one to see everything it produced. Start a new campaign from here.
- New Campaign: onboarding a new client or a new project for one. Four steps, ends with the generated script, flyer copy and landing page copy.
- Brand Assets: logo, colours, product images, past winning ads, reviews, testimonials, pages and reports. The agent uses these in videos, flyers and pages.
- AI Videos: opens straight on the video types. Generate from a campaign you have written (its script, offer and brand assets) or describe the product and offer right there.
- AI Graphics: generate a flyer from the campaign's flyer copy, or type the flyer copy there.
- Landing Pages: build from the campaign's landing page copy, or describe the business there. Add proof, build, publish.
- Click the logo to fold the menu to icons.

## How the campaign feeds the other screens
The campaign is the single source. AI Videos, AI Graphics and Landing Pages only send `campaign_id` plus the owner's choices (concept, format, product photo, reviews). The backend reads the script, flyer copy, landing page copy, chosen offer and brand assets from the campaign record. If a campaign has no script yet, the screen points the owner back to New Campaign step 4.
