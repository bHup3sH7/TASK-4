# what i learned building this

this started as a simple image + button layout. it ended up teaching me more about how browsers actually think than i expected.

---

## viewport units

`vw` and `vh` are percentages of the screen, not the parent element. that distinction matters more than it sounds. when i wrote `margin-left: 25vw`, i wasn't saying "25% of this section's parent" — i was saying "25% of the actual screen width". it's absolute in a responsive way, which is a weird thing to get your head around at first.

`vh` for height felt natural for the image (`height: 60vh`) because i wanted it to feel proportional to the screen, not to some container i'd have to manually size. but it also means if someone opens this on a very short screen, the image shrinks. that's either a feature or a bug depending on how you look at it. i'm still not sure which.

---

## the box model doing the actual work

the honest thing i learned here is that i was reaching for `display: grid` and `place-items: center` as a reflex, not because i needed them. when i stripped all that out, the layout still worked — because block elements just stack. that's the default. the browser already knows how to put a div below another div.

`width: 100%` on the button makes it fill its parent. the parent fills the section. the section is sized with viewport units. that chain is the whole layout. no grid needed.

margin positions the card on the page. padding adds breathing room inside. those two things together are genuinely most of what layout is. i keep forgetting that.

---

## what was actually hard

centering vertically without grid or flexbox is annoying. `margin-top: 10vh` on the section gets close but it's not true vertical center — it's just "push it down 10% and hope the content height works out". for this layout it looked fine. for something taller it would break.

i also kept second-guessing whether `width: 100%` on the image and button would cause horizontal scrollbars. it didn't, because `box-sizing: border-box` makes sure padding and border don't add to the width. but i had to consciously remind myself of that instead of just knowing it.

and `display: block` on the image — i always forget that `img` is inline by default, which leaves a small gap underneath it. adding `display: block` removes that gap. it's a small thing but it bit me once and i had to look it up to remember why it happens.

---

## what i'd do differently

i'd reach for viewport units earlier instead of mixing pixels and percentages and then wondering why things look off at different screen sizes. once everything is in `vw`/`vh`, the proportions just hold.

and i'd trust the normal document flow more. the instinct to immediately wrap things in a grid container and center everything is strong, but sometimes the browser's default stacking behavior is exactly what you need.
