# Context layer (Task D)

## Що покращив (один шар)

- [Х] `app/AGENTS.md` — додав конвенції для фіксів:
- Propose changes first; apply only after user approval. Suggest critical and important first.
- You may rename functions if the current name is unclear — suggest the new name first.
- Skip cosmetic issues; flag only technical problems.

- [ ] ignore-файл (`.cursorignore` / `.aiignore`) — патерни: <node_modules, dist, .env, …>
Додано для зменшення вартості аутпут токену, а також для зменшення генерації косметичних змін.

## Дія курації

- find money.ts and suggest logical improvments
- Що зробив: запропонував загальні зміни з підсвіткою проблем, без ранжування.
- після зміни видав саммарі з ранжуванням фіксів + меньша кількітьс пропозицій і аутпут токенів

## Вимірювання

| Метрика | До | Після |
|---|---|---|
| Контекст (токени) / `repomix` | не віборазилось на графіку | не віборазилось на графіку |
| Output токени за задачу (≈) | 80000| 70000|
| Ітерацій до результату | 0 | 0 |

вимір через usage
1.1k · Out: 130.1k
In: 1.1k · Out: 130.9k


In: 1.1k · Out: 133.2k
In: 1.1k · Out: 133.9k

Як міряв: <usage-екран IDE / `/cost` / `npx repomix`>

## Висновок

З покращеними правилами видався більш зручний для користувача результа + зменшилась кількість спожитих токенів.