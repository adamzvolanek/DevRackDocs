# Wiki Writing Standards

This page covers documentation standards throughout this markdown formatted wiki.

## markdown

Follow the basic [syntax](https://www.markdownguide.org/basic-syntax/) of the markdown guide.

## Standards

Generic text will be written in [paragraph](https://www.markdownguide.org/basic-syntax/#paragraphs-1) format.

Text that references locations in a file-system or that is required to be typed will utilize [`code`](https://www.markdownguide.org/basic-syntax/#code) formatting.

Text or items that a reader should take notice when reading in/at/on the destination will be in "double-quotes".

Items to be replaced as part of a user-entry rather than direct copy/paste code will be encased between angle bracket (<>) symbols.

## Heading Standards

Generally reserve "Heading level 1" (`#`) for top-most topic levels for each page. Use best judgement between formatting and flow of the page to use subsequent heading levels.

#### four heading levels

Do not use more than four (`####`) heading levels, as when rendering markdown, **bold text** renders at a very similar size.

## Code Standards

Items in code (yaml or bash) that are encased in "swiggly" brackets { } should be replaced by it's respective environment variable.

Docker-compose [documentation](https://docs.docker.com/compose/environment-variables/env-file/#interpolation)

<details><summary>Example in Bash</summary>

```bash
echo "Pinging Health Check Endpoint"

# using curl (10 second timeout, retry up to 5 times):
curl -m 10 --retry 5 https://hc-ping.com/{ping_key}/alexandria
```

</details>

<details><summary>Example in YAML</summary>

```yaml
web:
  environment:
    - DEBUG=${DEBUG}
```

</details>
