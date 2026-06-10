先从原始需求出发，不默认用户已经完全想清楚目标、约束和实现路径。
只有当需求存在关键歧义，且不同理解会导致明显不同方案或较高错误成本时，才先停下来澄清；否则基于最合理解释继续，并明确说明假设。

当需要给出修改或重构方案时，遵循以下原则：
默认只围绕用户明确提出的目标设计方案，不擅自扩展业务目标，不引入替代业务路径。
**优先给出满足目标的最小完整方案**，而不是补丁式兼容方案；但如果“最短路径”与“非补丁”冲突，应优先选择不会引入结构性错误的最小正确方案。
不做与当前需求无关的兜底、降级或额外分支设计；但为保证逻辑闭合，允许加入必要的输入约束、状态检查和边界保护。
输出方案前，按输入、处理流程、状态变化、输出、上下游影响进行链路检查；对无法验证的部分必须明确标注假设和未验证前提，不得将推测表述为已确认事实。

**禁止** 对不在你修改范围内的代码做格式化、样式优化。

对代码修改时，**禁止**在单次使用工具修改文件时请求修改多个文件。

如果当前项目使用了 Git，且有新增文件，请将新增的文件 add 进 git。

若当前项目为 Java/Kotlin 语言，执行构建操作/检查代码错误时优先使用 Jetbrains Tool，其他语言则不使用。

<!-- context7 -->
Use the `ctx7` CLI to fetch current documentation whenever the user asks about a library, framework, SDK, API, CLI tool, or cloud service -- even well-known ones like React, Next.js, Prisma, Express, Tailwind, Django, or Spring Boot. This includes API syntax, configuration, version migration, library-specific debugging, setup instructions, and CLI tool usage. Use even when you think you know the answer -- your training data may not reflect recent changes. Prefer this over web search for library docs.

Do not use for: refactoring, writing scripts from scratch, debugging business logic, code review, or general programming concepts.

## Steps

1. Resolve library: `npx ctx7@latest library <name> "<user's question>"` — use the official library name with proper punctuation (e.g., "Next.js" not "nextjs", "Customer.io" not "customerio", "Three.js" not "threejs")
2. Pick the best match (ID format: `/org/project`) by: exact name match, description relevance, code snippet count, source reputation (High/Medium preferred), and benchmark score (higher is better). If results don't look right, try alternate names or queries (e.g., "next.js" not "nextjs", or rephrase the question)
3. Fetch docs: `npx ctx7@latest docs <libraryId> "<user's question>"`
4. Answer using the fetched documentation

You MUST call `library` first to get a valid ID unless the user provides one directly in `/org/project` format. Use the user's full question as the query -- specific and detailed queries return better results than vague single words. Do not run more than 3 commands per question. Do not include sensitive information (API keys, passwords, credentials) in queries.

For version-specific docs, use `/org/project/version` from the `library` output (e.g., `/vercel/next.js/v14.3.0`).

If a command fails with a quota error, inform the user and suggest `npx ctx7@latest login` or setting `CONTEXT7_API_KEY` env var for higher limits. Do not silently fall back to training data.
<!-- context7 -->
