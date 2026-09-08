# Identified Issues for ffmpeg-skill

## Summary
Found 5 issues during code review. Issue #100 (Windows drawtext crash) is already reported.

## New Issues to Create

### Issue 1: Python 3.14+ SyntaxWarning on invalid escape sequence
- **File**: `_common.py:342`
- **Problem**: `" \t\\"'\\;|&<>()[]{}$*?"` contains invalid escape sequence `\;`
- **Severity**: Medium (will become error in Python 3.14+)
- **Fix**: Use raw string or properly escape

### Issue 2: Windows Python documentation gap
- **Location**: README examples, SKILL.md
- **Problem**: Examples show `python3` but Windows Git Bash only recognizes `python`
- **Severity**: Low (confuses Windows users)
- **Note**: `bin/install.js` handles this correctly; docs should too

### Issue 3: FFmpeg capability detection incomplete for drawtext
- **Problem**: `doctor` reports `missing required: none` but `drawtext` crashes at runtime on Windows
- **Severity**: High (violates design principle of early failure detection)
- **Suggested fix**: Add runtime probe to `doctor` for drawtext

### Issue 4: Font error messages lack context
- **Problem**: Fontconfig errors don't indicate actual cause (missing fontfile, invalid fonts.conf)
- **Severity**: Medium (hard to debug)
- **Impact**: All drawtext tools (look.py, scenes.py, overlay.py, graphics.py)

### Issue 5: SKILL.md missing Windows drawtext limitations
- **Location**: SKILL.md Gotchas section
- **Problem**: No mention of Windows-specific `drawtext` + fontconfig issues
- **Severity**: Medium (Windows users encounter Issue #100 with no warning)
- **Suggested addition**: Document fontfile= requirement on Windows

## Related
- Issue #100: "drawtext access-violates on Windows" (currently open)
