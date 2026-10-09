# hansenhunt.com: working notes for Claude Code

Read this first. It is the memory for this site across sessions. The repository is
public, so nothing here or in `docs/` may be confidential. Internal notes (pricing
arrangements, partner specifics not meant for the web) live in a private Claude Doc in
Hansen's account titled "Connection by Hansen: internal notes".

## What this is

Hansen Hunt's personal site, the public face of the umbrella brand "Connection by
Hansen". One static page, `index.html`, with inline CSS and a small inline script. No
framework, no build step, no analytics. Hosted on GitHub Pages from `main` at the root
(`CNAME` is `hansenhunt.com`, `.nojekyll` present). Every push to `main` deploys within
about a minute. HTTPS is enforced in the Pages settings.

The one third-party script is HubSpot Forms, loaded only when someone opens the contact
popup (portal 303888, form 54c40da1-4fbb-4acf-9a3c-21901a546821, region na1). Hansen
styled the form inside HubSpot to match the site.

## Workflow Hansen expects

- Make changes, render at 390px and 1280px with headless Chromium (Playwright is
  available; scripts in the session scratchpad are throwaway, write a new one), check
  tag balance and image references, then show Hansen a diff or screenshots when he asked
  for review. When he says "commit", commit and push; when he says "don't wait", deploy.
- Commit messages: file-based (`git commit -F`), author `Hansen Hunt
  <302689597+hansen-hunt@users.noreply.github.com>` because his GitHub email is private.
- Never add analytics, frameworks, or a build step. Keep the page fast: images are
  WebP with JPEG fallback, two sizes with `srcset`, explicit width/height, lazy below
  the fold.
- Put copy in the voice described in `docs/connection-crew-badge-tech.md` (warm, plain,
  no em dashes, no exclamation points, "team" and "teammate", "the person you're meeting").

## Page structure (top to bottom)

1. Sticky nav: H mark + two-line serif wordmark ("Connection / by Hansen Hunt"), links
   Work with me, About, What I do, Let's Connect. Logo starts 56px and shrinks to 34px
   on scroll. Hamburger menu under 40rem.
2. Hero on the Dawn gradient: big H mark (desktop only), H1 "Hansen Hunt", lede, Let's
   Connect button, and an arch-shaped photo (Balboa Park arches, Hansen speaking).
3. Services, "Five ways to bring more connection into the room", order fixed by Hansen:
   Event activations, Connection Crew (double-width, with a People / Technology strip
   for the Covve badge technology), Circles, Connection Buddy, Speaking (last, on
   purpose; Hansen does not want to be positioned as a keynote speaker).
4. "The idea behind the work": thesis "Resilience is relational.", two paragraphs, the
   Care Pathway pill strip, closing line "Low-stakes connection creates high-stakes
   capacity.", and a time-boxed Upcoming note between `<!-- upcoming:start -->` and
   `<!-- upcoming:end -->` for the Nov 12, 2026 Big Idea Night with Sara Schairer.
   Delete that block after the event.
5. About: headshot, pronouns, biography paragraphs (do not edit the biography without
   being asked), Connection Buddy sentence after the Chamber of Connection paragraph.
6. Longer Tables band: navy split layout, caption left, Botanical Building photo right.
7. What I do: three pillars with affiliations.
8. Let's connect (navy) with the social links; a commented placeholder for the
   Connection by Hansen LinkedIn Company Page URL.
9. Footer: "Connection by Hansen", the tagline, domain, city.
10. `<dialog id="connect-modal">` with the HubSpot embed. All mailto CTAs open it; the
    mailto stays as the no-JavaScript fallback.

## Copy rules Hansen has set

- Title is "connection experience designer", never "connection designer".
- Brand name "Connection by Hansen" appears in the nav wordmark and footer only. `<title>`
  and og:title stay "Hansen Hunt". H1 stays "Hansen Hunt".
- Tagline: "Designing experiences and communities where people feel seen, make real
  friends, and build their support systems."
- Core language to keep verbatim: "Resilience is relational." / "Connection creates the
  pathways. Compassion moves care through them. Repeated action builds shared capacity.
  That capacity is community resilience, and we build it before we need it." /
  "Low-stakes connection creates high-stakes capacity." / "A community capable of hard
  things." / "feel seen, heard, valued, and understood".
- Speaking is de-emphasized: no "keynote", talks are "usually with Sara", card last.
- Connection Buddy is not live. Never link to getconnectionbuddy.com or the old
  spaces.sdchamberofconnection.org from this site. Use "coming soon" language. Do not
  use "trusted", "verified", "AI", or "app" in Buddy copy. It helps San Diego club and
  community leaders find a place to meet.
- Keep off the site: neighbor names or health situations, the Norman story, the insulin
  pump, the family with a cancer diagnosis, "protest" framing. Those belong in the talk.
- Connection Crew: full name "Connection Crew by Covve" on first mention in a context;
  "badge technology by Covve", never "Cove". Never state pricing.

## Image pipeline

Originals are in `assets/photos/` (see its README for the inventory and usage map).
Web crops are in `img/`. Regenerate with ImageMagick, for example:

    convert in.jpg -auto-orient -crop WxH+X+Y +repage -resize 800x600^ -gravity Center \
      -extent 800x600 -strip -interlace Plane -sampling-factor 4:2:0 -quality 80 out.jpg
    convert in.jpg ... -quality 78 -define webp:method=6 out.webp

Sizes in use: hero 960x1200 and 1440x1800 (4:5, arch mask); cards 800x600 and
1200x900 (4:3, rendered as duotone in each card's tint via CSS, see `.card-photo`);
band 900x1200 and 1350x1800 (3:4, shown whole); portrait 600x750 and 900x1125.
No photo is used twice on the page.

## Open items (Oct 2026)

- Circles card has no photo; Hansen wants the boat-bow circle photo, not yet received as a file.
- LinkedIn Company Page URL for the footer links (placeholder comment in place).
- A dedicated page for the Covve badge technology / Connection Crew, built from
  `docs/connection-crew-badge-tech.md`.
- Connection Buddy card CTA once the product has a public home.
- Remove the Upcoming block after Nov 12, 2026.

## Related repositories

`hansen-hunt/gather-san-diego` holds the Chamber of Connection / Connection Buddy app
and its own CLAUDE.md. That is a separate codebase with separate rules.
