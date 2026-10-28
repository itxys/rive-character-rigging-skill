# Rive Character Rigging Skill

An open-source Codex skill for editing and checking expressive 2D Rive character rigs with the Rive CLI. It covers body variants, limb alignment, IK, crouches, jumps, facial acting, timing, and native visual review.

The skill grew from hands-on character animation work. It contains instructions and diagnostic lessons, not character artwork, Rive project files, or finished animations. It does not generate a polished performance from a prompt alone; an editable Rive source and visual iteration are still needed.

## Install

Clone this repository and copy its contents to your Codex skills directory as `rive-character-rigging`:

```powershell
git clone https://github.com/itxys/rive-character-rigging-skill.git
Copy-Item -Recurse -Force .\rive-character-rigging-skill "$env:USERPROFILE\.codex\skills\rive-character-rigging"
```

If that destination already exists, review your local changes before replacing it. The [Rive CLI](https://rive.app/docs/cli/getting-started) must be installed separately.

## Contents

- [`SKILL.md`](SKILL.md): the agent workflow and verification checks.
- [`references/character-motion-lessons.md`](references/character-motion-lessons.md): reusable motion and rigging lessons.

## License

MIT. See [LICENSE](LICENSE).
