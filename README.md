# openapi-diff-action
A GitHub Action to identify differences between OpenAPI specifications. It uses [OpenAPITools/openapi-diff](https://github.com/OpenAPITools/openapi-diff).

## Usage

The following example [workflow step](https://help.github.com/en/actions/configuring-and-managing-workflows/configuring-a-workflow) will generate JSON and Markdown difference contents.

```yml
- name: "Find difference between OpenAPI specifications"
  id: diff_state
  uses: swimmwatch/openapi-diff-action@v1
  with:
    old-spec: "old_spec.json"
    new-spec: "new_spec.json"
    json: "out.json"
    markdown: "out.md"
- name: "Print difference state"
  run: echo "Current state: ${{steps.diff_state.outputs.state}}."
```

## Options
The following input variables options can/must be configured:

|Input variable|Necessity|Description|Default|
|----|----|----|----|
|`old-spec`|Required|Path to old version OpenAPI specification.||
|`new-spec`|Required|Path to new version OpenAPI specification.||
|`header`|Optional|Use given header for authorization. Format: `<property=value>` |`''`|
|`query`|Optional|Use given query for authorization. Format: `<property=value>` |`''`|
|`log`|Optional|Use given level for log. Expected values: (`TRACE`, `DEBUG`, `INFO`, `WARN`, `ERROR`, `OFF`) |`ERROR`|
|`markdown`|Optional|Export diff as markdown in given file. |`'.tmp/markdown'`|
|`json`|Optional|Export diff as JSON in given file. |`'.tmp/json'`|
|`text`|Optional|Export diff as text in given file. |`'.tmp/text'`|
|`html`|Optional|Export diff as HTML in given file. |`'.tmp/html'`|
|`fail-on`|Optional|Fail if API changed but is backward compatible (`changed` value) or changes broke backward compatibility (`incompatible` value). |`''`|

## Outputs
- `state`: Output diff state: `no_changes`, `incompatible`, `compatible`.

## License
openapi-diff-action is licensed under the [MIT License](LICENSE).