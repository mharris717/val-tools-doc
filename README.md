# Val Tools

I wrote something to let me use Vals as tools for LLM calls. 

## Writing a tool

A Val Tool is an HTTP Val that exposes two endpoints:

### POST /

Calls the tool

### GET /schema

Serves a JSON schema for the request payload

### Example

Fetches body of specified file in a github repo

<iframe width="100%" height="400px" src="https://www.val.town/embed/mharris717/githubFileTool" title="Val Town" frameborder="0" allow="web-share" allowfullscreen></iframe>

```
export const FileIdentSchemaProper = z.object({
  repo: z.object({
    owner: z.string().describe("Repo Owner"),
    repo: z.string().describe("Repo Name"),
  }),
  ref: z.string().describe("git sha or branch name"),
  file: z.string().describe("relative path within repo"),
}).describe("Github File to read");
```

### Hono Helper

Accepts a method to execute and a Zod schema
Returns a Hono app meeting the spec

<iframe width="100%" height="400px" src="https://www.val.town/embed/mharris717/makeHonoTool" title="Val Town" frameborder="0" allow="web-share" allowfullscreen></iframe>

## Using the tool

This is the main code for connecting a Val Tool to an LLM call. This is uses the Vercel AI SDK, but the concept makes sense regardless. 

<script src="https://gist.github.com/mharris717/695e4e9572998e70d65c74221abce40d.js"></script>
