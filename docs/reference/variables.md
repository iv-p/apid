# variables

## Summary

Variables are scoped either globally, to a transaction or to a step. Variables in a narrower scope have precedence over those in a broader one. Variables are available in templates - `"{{ var.api_url }}"`. Make sure to add quotes to it so that the YAML parser doesn't confuse it for a YAML object.

## Regular variables

These are declared either in the transaction, step or the root yaml document. There they are simply declared as a mapping from variable name to its value. Those will be available in templates using the `var` prefix - `"{{ var.api_url }}"`

## Exported variables

Each step can export a set of variables. This is useful when you want to make a request and then use part of the response in another request. For example, when you authenticate to get a token and then use this token in subsequent requests. See [step](https://github.com/getapid/apid-cli/tree/22534ec0dafbcd65c14c4b649fbab9b5f7ae7398/docs/step/README.md) about the exact syntax of exporting variables in a step. Exported variables will be available in subsequent steps by using the step id that exported them; e.g `"{{ step_one.auth_token }}"`

## Environment variables

These will contain anything environment variable that the APId CLI has inherited. Useful for injecting passwords or other kinds of secrets. They will be available like so: `"{{ env.PASSWORD }}"`

## Examples

```yaml
variables:
  title: 'A long time ago'
  subtitle: 'in a {{ var.place }} far far away {{ env.DATABASE_USER }} accidentally dropped all tables'
  year: 2187
```
