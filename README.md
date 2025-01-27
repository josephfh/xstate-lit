# xstate-lit

Connect XState machines with Lit Element components. Similar to `@xstate/react`'s useSelector hook.

Based on @ChrisShank's PR https://github.com/statelyai/xstate/pull/2581

## Setup

`npm install --save xstate-lit`

## Example

```ts
export class MyElement extends LitElement {
  count = new SelectorController(this, actor, (state) => state.context.count);
  render() {
    return html` <div>count is ${this.count.value}</div> `;
  }
}
```

To run example install node_modules at top level as well as in example directory:

```
pnpm install
cd example
pnpm install
pnpm run dev
```

## SelectController

This Lit ReactiveController:

1. Subscribes to all updates of an XState actor or service.
1. Runs the user provided state selector function when the state changes or the actor receives an event.
1. Triggers the Lit component to update if the compare function returns false. The default compare function uses `===` to check equality of the old and new selected values.

## SelectState

A wrapper for SelectController that pulls the XState actor or service from a `@lit-labs/context`. This avoids needed to pass a shared actor down the component tree.
