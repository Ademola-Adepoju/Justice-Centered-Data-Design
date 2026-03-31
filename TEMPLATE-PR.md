# CHAPTER X.x - Firstname Lastname

## Triumphs

1. **Nolving the * * * * * Breaks**: The * * * * * section breaks wouldn’t disappear with a simple replaceAll. The text had extra spaces/newlines, so my match kept missing. After a bit of research I found that  a small regex (and also tried a split → filter → join approach) to strip any line that was just five asterisks; it worked, and I’m happy I solved it. However, I'm still curious if there’s an even simpler, non-regex way to do the same cleanup. This regex way feels somehow daunting.
