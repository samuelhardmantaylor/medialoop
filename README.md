# medialoop website

A one-page scrolling site. No build step and no dependencies: `index.html` plus the `assets` folder.

## Put it on GitHub Pages

1. Create a new repository on GitHub (for example `medialoop`).
2. Upload everything in this folder (`index.html`, `assets/`, `.nojekyll`, this README) to the repository's main branch.
3. In the repository, open **Settings → Pages**. Under **Build and deployment**, choose **Deploy from a branch**, pick `main` and `/ (root)`, and save.
4. After a minute the site is live at `https://<your-username>.github.io/<repository-name>/`.

For your own domain (for example `medialoop.org`), add it under **Settings → Pages → Custom domain** and follow GitHub's DNS instructions.

## Editing

Everything you will want to change is plain HTML in `index.html`:

- **Description**: the `lede` paragraph under the logo and the `statement` paragraph in About.
- **About cards**: the three `<article>` blocks.
- **Publications**: each `<li>` in the `pubs` list. Put the paper's link in `href="#"`.
- **People**: each `<article class="card">` (there are five). Edit the `h3` (name) and the `role` paragraph. To add a photo, put `<img src="assets/people/name.jpg" alt="Name">` inside the empty `photo` div; it takes on that card's organic outline automatically. The faint net print on the cards is drawn from the same net as the background.
- **Person pages**: each person can have their own page in the `people` folder. Samuel's is `people/samuel-hardman-taylor.html`, and his card on the home page links to it. To add one for someone else, copy `people/_template.html`, rename it (for example `people/jane-doe.html`), fill in the name, role, bio, research interests, publications and links, then on the home page change that person's `<article class="card">` … `</article>` to `<a class="card" href="people/jane-doe.html">` … `</a>`. To add a photo, follow the comment above `p-photo` in the page. Person pages use a sidebar layout: on wide screens a tall blue column on the left (`.p-side`) holds the photo (an organic blob with a soft shadow), name, role and links, and stays in place while the page scrolls beside it; the net fills generous bands at its top and bottom with swaying inner edges and always keeps clear of the photo, text and menu button (`drawSide()` in the script). Where the blue meets the cream page it ends in a natural, slightly uneven brush-stroke edge (set as a clip-path in the script). On narrow screens the column becomes a blue header block, and the top bar turns see-through and cream while it is over it. The photo floats, the letters of the name bounce on hover, and research interests sit on the net's own hole shapes, stretched long, floating gently and turning gold on hover.
- **Section headings**: each `<p class="label">` is a big, bold, tight heading (like "Events") ending in a gold full stop, with a small uppercase kicker above it set by its `data-kicker` attribute (for example `<p class="label" data-kicker="Who we are">People</p>`). The heading rises in and the full stop pops in when it scrolls into view.
- **Entrances**: the About columns, publications, people cards, contact lines and footer fade and rise gently into place as they scroll into view, a little staggered (the cards also settle from a slight tilt). Visitors with reduced motion turned on see everything without movement.
- **Bold words**: wrap any words in `<span class="t5">…</span>` (medium) or `t6` (semibold); `t2` makes them extra light.
- **Colours**: the main text and logo colour is `--blue:#2c5494` at the top of the styles (the logo file `assets/medialoop-wordmark.svg` uses the same value).
- **Email**: the `mail` link in the Contact section.

## The net and the gradient

The net is drawn from the hole shapes of your fine net, stored in `assets/net-holes.js` (with a copy in `assets/net-holes.json`). Keeping it as a script means the net also shows when you open `index.html` straight from a folder on your computer. The holes never move; they breathe, swelling and shrinking in slow ripples. Under the net, a tone-on-tone blue gradient drifts inside a soft glow.

The net belongs to the page rather than the window. At the top it sits beside the logo; as visitors scroll it slides up to the top-left corner and scrolls away with the top of the page, and it is back when they scroll all the way up. A second net, wider and thinner, sits in the space between About and Publications and slides from left to right as visitors scroll past; and a third belongs to the Contact section, on the left just above the heading. Each scrolls with its part of the page. Behind the logo and behind the contact text there is a soft cream fade, so both read cleanly over the net. Their positions are set in the `target()` function in the script.

Each section's `data-net="x y r"` sets where the glow sits for that section (x and y are fractions of the window, so values below 0 or above 1 are off screen; r is its size, and 0 hides it). `data-net-m` is the same for phones. The optional `data-net-at="a b"` says exactly when that spot is reached: when the point `a` of the way down the section (0 = its top, 1 = its bottom) reaches `b` of the way down the window.

To change the gradient, edit the `BLUES` list in the script: colours with their angle, distance from the centre, size and drift speed.

## The opener

The opener follows the visitor's scrolling (mouse wheel, trackpad, touch or arrow keys) rather than a timer. The net fills the screen on load; as visitors scroll it gathers back into its glow beside the logo while the page fades in, and scrolling back up plays it in reverse until the page is reached. On phones and tablets the net follows your finger, and a single swipe up finishes the opener; the page itself only scrolls when you swipe again. If nobody scrolls for a few seconds it carries on slowly by itself. It plays once per visit: going back, reloading or returning from a person page goes straight to the page. It is also skipped for visitors who have reduced motion turned on. To remove it, delete `class="intro"` and `data-opener="eye"` from the `<html>` tag and the `<div id="intro">` block.

Every round shape on the page (section bullets, marquee dots, people circles) gets its own irregular, soft-edged outline when the page loads, so no two are alike.

## Menu
On every screen size the section links fold into a menu button (three lines, top left; the logo sits top right). Tapping it slides a cream panel in from the left: on desktop a narrow panel (about 400px) over a lightly dimmed page, on phones the full width. Tapping a link, the X, beside the panel, or pressing Escape closes it. The styles live in the "menu: a button that opens a full-screen pop-out" block in each page's `<style>`, and the same markup is in `people/_template.html`, so new person pages get it automatically.

## Opener: cue, dots, auto-advance
While the opener is on screen, a large gold dot with a small blue up mark breathes at the bottom: it starts round and, as the opener gathers, sweeps out wide and up over the page, swelling mid-flight, while its outline morphs into the logo's i-dot; it lands as the dot on the i (the logo shows `assets/medialoop-wordmark-nodot.svg` until it lands). If nobody scrolls for 5 seconds, the opener carries on to the home page by itself. As it gathers, gold, cream and pale-blue dots fly in from the edges and settle into the net beside the logo; their number, sizes and colours are in the `FLY` list in the script. The gold heading bullets are now drawn as vector shapes (`vecBlob`), so they stay sharp.
The opener's background is a wide gradient made only from shades of the logo blue (#2c5494): from #142643 through #1e3a66 to the logo blue itself, with lighter #3a6ab6, #6a8ec8 and #a5b9d9 pools drifting over it. It slowly turns. Set in `drawLace()` under "a wide blue-on-blue sweep".


## Person pages always open at the top
A small script in each person page's `<head>` scrolls to the top on load (unless the link has a `#section`), so a page never opens part-way down, even inside previews that remember the scroll position.


## The word banner between About and Publications
A blue-on-blue band, tilted 10 degrees (lower on the left), with smooth, very slightly uneven edges, like one quick brush stroke and cream medialoop wordmarks gliding from right to left and a small gold dot between each. The wordmarks nearly fill the height of the band, leaving a thin strip of blue above and below. They drift slowly on their own and speed up gently as you scroll (and ease back if you scroll up). The tilt, band height (`--bh`) and colours are in the `.wband` CSS; the movement is `wordBand()` in the script.


## Research interests (person pages)
Four square cards in the style of the people cards: the real net (blue with breathing cream holes) fills the top of each card and fades out above the words. Each card has one tight, bold title in cream. To add or change one, copy a line like `<li><canvas aria-hidden="true"></canvas><strong>Your interest</strong></li>`. Each card takes its own colour in turn (blue, gold, deep blue, cream) with the net in the matching contrast colour, like the people cards; on hover it lifts and leans.


## People cards (home page)
The same style as the research interest cards: the real net breathing in the top of each card around the photo, fading out above the name. Name in bold, tight Inter at the bottom left, role below. Gold with a lean on hover. Each photo has a thin cream rim and a soft shadow, and the net clears away around it so faces stay easy to see. The net is drawn by `drawPeople` in the script. To add a photo, put `<img src="assets/name.jpg" alt="">` inside the card's `.photo` box (a square, head-and-shoulders crop works best).

## Opener: the wordmark written into the net
As the page opens, the medialoop wordmark is written into the net in cream, left to right, in about 1.4 seconds. The net stays all around the word, but no bubble ever touches a letter: each bubble near a stroke is nudged away and shrunk so it keeps a small clear gap, any that would be too squeezed disappear, and the loops of the letters stay empty. A small ripple runs out from the pen as it writes. The word fades as the net gathers into the glow beside the heading. See `writeState()` (size, speed, how far bubbles part) just above `drawLace()`.
The writing has a soft, feathered pen edge and eases out (about 1.9 seconds). The word breathes in place with the net (a slow, slight swell). The bubbles around it never move: each is capped to a size that keeps a clear gap from the letters, and any that would be too small is not drawn, so nothing sits behind the word or flickers. The word itself is a sharp vector element laid over the net (`#writeMark`), so it stays crisp on any screen.
Bubbles next to the letters ease away smoothly: distances are measured on a smooth field (no stepping as the word moves), the loops of the letters fade out gently, and a bubble that has to leave dissolves rather than shrinking to a flickering speck.


## Opener: the net becomes the wordmark
Corners: the blue gradient fills the screen with the large cream logo, laid exactly where the blue logo sits on the home page (bottom left), so swiping simply turns it from cream to blue in place; it breathes slightly in and out, in time with the dots. "A Research Boutique" sits underneath in small, widely spaced Inter Light capitals. The net sits only in two round, slightly lumpy blots set just inside the top-left (larger) and bottom-right (smaller) corners, which drift slowly in and out; holes move away from the pointer and never come near the logo (see `cornerF()` and `clearF()` before `drawLace()`, and the `#openLock` element). The gold dot cue and the swipe-up transition are unchanged.

## Events
A full-width gold-on-gold gradient band (`#events`, lighter top left, deeper bottom right) after Publications with crisp, slightly uneven brush-stroke edges at the top and bottom (the same idea as the word banner, set as a clip-path in the script), a cream net over it, and four blue cards with cream type that turn cream with blue type on hover. The word "Events" is set like Apple display type (bold, very tight tracking, clean alternates) and, like the names on the people pages, each letter hops when you hover it. Each card has the breathing cream net in its top-right corner, like the resource cards. Edit the cards in the HTML; each has a when line, a title, a sentence and a where line. The net is drawn on a canvas at the screen's own resolution so the holes stay sharp; its cream is the `rgba(242,238,221,.88)` value in the script.


## Page order
After the opener and About, the home page runs: the medialoop banner, People, Events, Publications (with a "More research" button at the end), Resources, then Contact. The menu lists them in the same order.

## Research page
`research.html` is the full list of publications, linked from the "More research" button under Publications on the home page (a gold pill with blue type that turns blue on hover; it sits above the background net, and the net keeps clear of it). A huge, tight "Research" heading (each letter hops on hover), a short intro. Entries are grouped by year: each year is a big thin number that sticks beside its entries, pale until you reach it and then full blue. Titles thicken and get a gold underline on hover. Every entry is a placeholder for now: to add one, copy an `<li data-t="journal">` line inside the right year (`data-t` is `journal`, `conf` or `chapter`), and to add a year, copy a whole `<section class="r-year">` block. 

## Entrances and menu feedback
On the home page, the people pages and the research page, things fade and rise into place one after another as they come into view (the back link, photo, name, role, each link, headings, paragraphs, each card and each publication). When you tap a link in the menu, its gold dot swells, the word slides over and a gold line sweeps under it; the menu closes a moment later and takes you there.


## Resources
`#resources`, after Publications, uses the "Additional resources" text and links from samuelhardman.com: Survey Measures (the PARIS scale document), Open Science Framework, Truman (GitHub), Presentations and posters (Drive folder) and Research publications (pre-print Drive folder). The cards are all the same size and stack on top of one another as you scroll (sticky, each a little lower than the last); a covered card keeps a slim strip showing its name, so the finished pile reads as a list of all five and nobody has to scroll back through them. Each card has the breathing net on its right side. To add one, copy an `<a class="res ...">` block, set `--i` to its position and update the "0N / 05" counters; colours are `r-blue`, `r-blue2`, `r-gold`, `r-cream`, `r-ink` and `r-egg` (deep aubergine, used on Research publications). Each card's net has its own shape and hole size, from the `NETS` list in the script (the event and people cards vary the same way).

## Publications and bio
The home page, research page and Samuel's profile list the five research highlights from samuelhardman.com with their links (the Open Science in Communication paper has no link on that site, so it has none here). Samuel's bio comes from the same site. His profile links are his UIC profile, Google Scholar and CV; the CV link points to `assets/people/samuel-hardman-taylor-cv.pdf`, so drop the PDF in with that name.

## Photos
People photos are used as they are, in natural colour with their original background, cropped square; the site shapes them and adds the cream rim. Samuel's is `assets/people/samuel-hardman-taylor.jpg`.


## People cards
Cards are landscape (16:10): photo on the left, name and role on the right. They fill a grid of three across on wide screens, two on tablets and one on phones.
Every card is the same blue (so no one reads as different), with the breathing cream net, a big tight name, and the photo in an organic blob with a soft shadow (no rim). Each card shows just the person's name, large. On hover the card turns gold, lifts and leans, and the photo swells and turns slightly.


## Apply card
In Contact, after the email address: a big gold "Apply" card with blue type (same style as the resource cards, with the breathing net on its right) saying the collective is affiliated with UIC Communication and that PhD and Master's applicants are welcome. Its "More information" button goes to https://comm.uic.edu/academics/graduate-studies/prospective-students/ (the link used on samuelhardman.com).
