
## 🤖 Type Automation (Middle Ground)

We use `openapi-typescript` to ensure Type Safety between Backend (Python) and Frontend (TypeScript). This is a **read-only** process that generates interfaces based on your API.

### **How it Works**
- Backend: Python `Pydantic` models define the data structure.
- Generator: Reads `http://localhost:8000/openapi.json`.
- Frontend: Creates `apps/web/src/shared/api/schema.d.ts`.

### **Usage**
Whenever you change a Backend model, run this command to update Frontend types:
```bash
pnpm run gen:types --filter web
```

### **How to Remove (If you want to stop using it)**
If this automation causes "jamela" (trouble), you can remove it easily:
1. **Uninstall:** `pnpm remove openapi-typescript --filter web`
2. **Clean Script:** Open `apps/web/package.json` and delete the `"gen:types"` line.
3. **Delete File:** Delete `apps/web/src/shared/api/schema.d.ts`.
4. **Revert:** Go back to manually writing types in `types.ts`.


### **?? Docker Automation (Zero-Touch)**
We have configured Docker to handle this automatically.

**How it works:**
When you run `docker-compose up`:
1. The Web container waits for the API to be ready.
2. It automatically runs the generator.
3. Then it starts the website.

You don't need to do anything manually when using Docker! ??
