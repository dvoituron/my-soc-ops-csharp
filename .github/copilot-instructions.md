# Soc Ops — Project Guidelines

## Mandatory Dev Checklist
Before submitting any change, run these in order and fix all errors:
```bash
dotnet format --verify-no-changes SocOps/SocOps.csproj  # lint
dotnet build SocOps/SocOps.csproj                        # build
# no test project — add one before writing testable logic
```

## Overview
Social icebreaker bingo — Blazor WebAssembly on .NET 10. Players fill a 5×5 board of social prompts; first to 5-in-a-row wins.

## Architecture
```
Components/   # Razor UI: BingoBoard, BingoSquare, GameScreen, StartScreen, BingoModal
Data/         # Questions.cs — question bank
Models/       # GameState (enum), BingoSquareData, BingoLine
Pages/        # Home.razor — entry point
Services/     # BingoGameService (scoped state), BingoLogicService (static logic)
wwwroot/css/  # app.css — all utility classes
```

## Conventions
- `BingoGameService` raises `OnStateChanged` after every mutation; components call `StateHasChanged()`.
- `BingoLogicService` is fully `static` — no instance needed.
- CSS: utility classes only (`.flex`, `.grid`, `.bg-accent`, etc.) — no inline styles, no external frameworks.
- Components: `[Parameter]` for inputs, `EventCallback` for outputs. No service injection in leaf components.
- `<Nullable>enable</Nullable>` — always handle nullable reference types.

## Key Files
| File | Purpose |
|------|---------|
| `SocOps/Data/Questions.cs` | Question bank |
| `SocOps/Services/BingoGameService.cs` | State + localStorage persistence |
| `SocOps/Services/BingoLogicService.cs` | Board generation, win detection |
| `SocOps/Components/GameScreen.razor` | Main game view |
| `SocOps/wwwroot/css/app.css` | All utility CSS classes |

## Further Reading
- CSS utilities: `.github/instructions/css-utilities.instructions.md`
- Frontend design: `.github/instructions/frontend-design.instructions.md`
- Workshop: `workshop/`
