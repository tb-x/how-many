# How Many?

A maker for printable counting sheets for young kids (around age 5). Each sheet has a big box scattered with
small pictures of a few kinds (flowers, bees and snails in a garden; fish, crabs and shells in the sea…), and
underneath, one answer box for each kind. The sheets have no words, so they work for kids who can't read yet, and
they're made for a black-and-white printer. The answer is hidden in a QR code: scan it with a phone camera to watch
every picture get counted.

Live at **https://tb-x.github.io/how-many/**

## How it plays

- Print a sheet. The big box has 2 to 5 kinds of picture in it, scattered about and turned a little, never
  touching each other.
- Under the box there's one answer box for each kind, showing that kind's picture.
- Count each kind (ticking or colouring them in as you go helps), then either write the number in the empty box
  next to its picture, or colour that many dots, depending on how the sheet was made. The dots come in groups of
  five, so they're easy to count too.
- Every kind has a different number, so no two answers are the same.
- With **Tricky ones** turned on, a few lookalikes hide among them: a fly among the bees, a slug among the snails,
  an umbrella among the mushrooms, a star among the starfish. They have no answer box, so they don't count. Only
  count pictures exactly like the one in the answer box.
- Scan the QR code in the top right corner of the box. The answer page counts one kind at a time: each picture
  lights up with its number (1, 2, 3…), and when a kind is done its total pops into its answer box (as a big
  number, or as coloured dots). Any tricky ones fade first and get a grey ✕. Tap the picture to count again.

## The maker page

- **Kinds**: how many kinds of picture are in each box, 2 to 5.
- **Up to**: the most of one kind, 5, 10, 15 or 20. Each kind gets a different count, picked from about the top
  two thirds (up to 10 gives counts from 3 to 10, up to 20 from 6 to 20).
- **Answer with**: A number (an empty box with a faint line to write on) or Dots (a row of as many dots as
  "Up to", in fives, to colour one for each picture).
- **Pictures**: Garden (flower, bee, butterfly, ladybird, snail, mushroom), Sea (fish, shell, starfish, crab,
  octopus, turtle), Space (star, moon, rocket, planet, UFO, comet), Farm (pig, chick, sheep, carrot, tractor,
  apple), Sweets (lollipop, sweet, cupcake, ice cream, doughnut, cake), or A mix (each kind from a different
  set). Every picture is a black outline, so it can be coloured in.
- **Tricky ones**: None, A few (one kind of lookalike, 2 or 3 of it) or Lots (two kinds, 2 to 4 of each). Each
  lookalike is picked to match a kind in the box:

  | Kind | Tricky one |
  | --- | --- |
  | Flower, bee, butterfly | Sun, fly, dragonfly |
  | Ladybird, snail, mushroom | Spider or turtle, slug, umbrella or cupcake |
  | Fish, starfish, crab, octopus, turtle | Leaf, star, spider, jellyfish, ladybird |
  | Star, moon, rocket, planet, UFO, comet | Starfish, banana, carrot, ball, hat, balloon |
  | Chick, sheep, carrot, apple | Lemon, cloud, rocket, pear |
  | Lollipop, sweet, cupcake, ice cream, doughnut, cake | Balloon or flower, bow, mushroom, carrot, lifebuoy, drum |

  Shell, pig and tractor have no lookalike, and when the kinds in a box have too few between them, the maker picks
  other kinds.
- **Per page**: 1 or 2 boxes on each A4 page. The pictures are made as big as the box allows (up to 2 cm); 2 per
  page is greyed out when a crowded box would need pictures smaller than 1 cm.
- **Pages**: how many pages to print at once (up to 20).
- **New scenes** makes new boxes for every page, ↻ on a page makes new ones for that page only, and **Print**
  prints them. Changing the pictures keeps the same scenes. The settings are remembered in this browser.
- Clicking a QR code on screen opens its answer page.

The QR code holds the whole scene in the link, all as digits: the box's size, the picture size, the answer style,
"up to", then each kind's picture and count, then each tricky one's picture and count, then every picture's place on a 100 × 100 grid and how far it's turned
(5 digits a picture). Each picture's slight size difference comes from those same digits, so the answer page can
redraw the scene exactly. The digits go into the QR code in its numeric mode, which packs them tightly; a crowded
box still needs a bigger QR code, so it grows to keep every dot at least 0.4 mm (about 25 mm for 5 kinds of up to
20). Nothing is stored anywhere, so a printed sheet keeps working for as long as this page is online. The QR always
points at the published page on GitHub Pages, even when the maker runs on a local server.

## Running it

It's a single `index.html` with no build step. Serve the folder and open it:

```bash
python -m http.server 5221
```

Then go to http://localhost:5221/. Opening `index.html` straight from disk works too. The QR codes are made
by [qrcode-generator](https://github.com/kazuhikoarase/qrcode-generator) 1.4.4 (MIT), loaded from cdnjs.

After the first visit the page also works offline and can be added to a phone's Home Screen.

## Tuning knobs

Named constants at the top of the script in `index.html`:

| Constant | Default | What it does |
| --- | --- | --- |
| `DEFAULTS` | 3 kinds, up to 10, a number, Garden, no tricky ones, 1 a page, 1 page | Starting settings |
| `KINDS` | 2, 3, 4, 5 | The choices under "Kinds" |
| `UP_TO` | 5, 10, 15, 20 | The choices under "Up to" |
| `SHEETS_MAX` | 20 | Most pages printed at once |
| `TRICKY`, `TRICKY_MIN` | none / 1 kind of up to 3 / 2 kinds of up to 4; at least 2 | How many tricky ones each choice gives |
| `TRICKS` | see the table above | Which lookalikes can go with each kind |
| `COUNT_LOW` | 0.3 | Counts are picked from "up to" × this, up to "up to" |
| `PIC_MAX` / `PIC_MIN` | 20 / 10 mm | Biggest picture in a box, and the smallest that allows 2 boxes a page |
| `DENSITY` | 0.46 | How much of the box the pictures (with their gaps) are sized to fill |
| `GAP` / `FRAME_GAP` | 2.5 / 2 mm | Least space between two pictures, and between a picture and the frame |
| `SIZE_SPREAD` | 0.12 | Pictures are up to 12% bigger or smaller than the box's picture size |
| `TURN` | 25° | Most a picture is turned either way |
| `CANDIDATES` | 24 | Spots tried for each picture; more gives an even spread, fewer a clumpier one |
| `ANS_GAP` | 6 mm | Space between the box and the answer boxes |
| `ANS_PIC`, `BOX_W` | 20 mm, 1.45 | Picture size in a "write the number" answer, and the writing box's width in pictures |
| `NUM_CELL_MIN` | 40 mm | Narrowest writing answer before they go on two rows (5 kinds do) |
| `DOT_PIC` | 12 mm | Picture beside a row of dots |
| `DOT_MAX` / `DOT_GOOD` | 9 / 7 mm | Biggest dot, and the smallest that lets rows of dots sit side by side |
| `QR_SIZE` | 24 / 22 mm | Smallest answer QR code with 1 or 2 boxes a page |
| `QR_MODULE` | 0.4 mm | Smallest QR dot: crowded boxes get a bigger QR code so a phone can still read it |
| `COUNT_TIME`, `STEP_MIN` / `STEP_MAX` | 14 s, 0.16 / 0.5 s | Answer page: about how long counting everything takes, and the shortest and longest step |
| `KIND_PAUSE` | 0.9 s | Answer page: pause after each kind while its total shows |
| `COLOURS` / `TINTS` | red, blue, green, purple, orange | Answer page colours for each kind's numbers and pictures |
| `PUBLIC_URL` | `https://tb-x.github.io/how-many/` | Where the QR codes point |
