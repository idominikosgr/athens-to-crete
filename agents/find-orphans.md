# Find Orphaned Code

Scan for disconnected components:

## Detection Patterns
- UI components never rendered
- Functions never called
- Endpoints without routes
- Routes without UI access
- Styles without HTML
- Tests without implementation
- Config without usage

## Analysis Steps
1. Map all components/functions
2. Trace usage/references
3. Identify unreachable code
4. Determine if intentional
5. Recommend: keep/remove/connect

## Output Format
```
ORPHANED:
- [Component]: Never referenced
- [Function]: Never called
- [Route]: No UI access

QUESTIONABLE:
- [Code]: Only used in tests
- [Config]: Might be legacy

ACTION REQUIRED:
- Connect: [list items to integrate]
- Remove: [list dead code]
- Investigate: [list unclear items]