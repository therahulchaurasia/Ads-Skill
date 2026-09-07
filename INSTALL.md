# Install

## Claude Code - for all your projects

```bash
git clone https://github.com/therahulchaurasia/Ads-Skill.git ~/.claude/skills/ad-studio
```

Windows PowerShell:

```powershell
git clone https://github.com/therahulchaurasia/Ads-Skill.git "$env:USERPROFILE/.claude/skills/ad-studio"
```

Restart Claude Code. Type `/` and `ad-studio` should be in the list.

## Claude Code - for one project only

```bash
git clone https://github.com/therahulchaurasia/Ads-Skill.git /path/to/project/.claude/skills/ad-studio
```

Use this when the skill belongs to a client repo rather than to you. Project skills load for anyone working in that folder.

## Claude apps (claude.ai)

Clone it, then zip the folder and upload under **Settings, then Features**. Requires a Pro, Max, Team or Enterprise plan with code execution enabled.

The zip must have the skill folder as its root - zip `ad-studio` itself, not the directory containing it:

```bash
git clone https://github.com/therahulchaurasia/Ads-Skill.git ad-studio
zip -r ad-studio.zip ad-studio
```

One caveat worth knowing before you rely on it: this skill writes files - the brand profile, the spec, the finished ads. That works where there is a persistent working directory. In a plain chat surface the files live only for that conversation, so the brand gets re-asked next time and the spec cannot be re-run later. The ads still come out; the memory between sessions does not.

## Verify it loaded

Type `/` and look for `ad-studio`. If it isn't there:

- Confirm the path is `~/.claude/skills/ad-studio/SKILL.md`, not `~/.claude/skills/SKILL.md` and not nested one level deeper
- Restart the session - skills load at startup

## Use it

Nothing to configure. Drop a reference ad screenshot into your working folder and say:

```
I want to make an ad like this for my brand
```

You do not need to name the skill. It triggers on the intent.

## Updating

```bash
cd ~/.claude/skills/ad-studio && git pull
```

**A running session keeps whatever version it loaded at start.** Updating mid-conversation changes nothing until you restart. This catches people out - if a fix does not seem to have taken effect, that is almost always why.

## Uninstalling

```bash
rm -rf ~/.claude/skills/ad-studio
```

Your `.ad-studio/` working folders are untouched - brand profiles, specs and finished ads all stay where they are.

## Troubleshooting

**It doesn't trigger.** Say what you want in plain language ("make an ad like this for my brand") rather than naming the skill. If it still doesn't fire, invoke it directly with `/ad-studio`.

**It used the wrong brand.** `.ad-studio/brand.json` from a previous project is in that folder. Say so - it archives the old profile and starts fresh. Or work in a new folder.

**No image appeared.** No generator is connected. That's expected and handled: you get a prompt pack instead - the prompt, the copy and the size - written next to where the image would have gone.

**The output looks generic.** Usually the reference. Busy or low-contrast references translate badly. Try a cleaner one in the same format.
