# Reproduction


```
npx ember-cli addon ec-addon-docs-repro --yarn
cd ec-addon-docs-repro
yarn
```

## [https://ember-learn.github.io/ember-cli-addon-docs/docs/quickstart](https://ember-learn.github.io/ember-cli-addon-docs/docs/quickstart)

```
ember install ember-cli-addon-docs
# choose ESDoc or install below
ember install ember-cli-addon-docs-esdoc
```

following the rest of the quickstart, ignoring template linting errors.

during the `ember generate docs-page usage` step,
fix the router:
```js
Router.map(function() {
  docsRoute(this, function() { /* Your docs routes go here */ });
  this.route('usage');
});
```
should be
```js
Router.map(function() {
  docsRoute(this, function() { 
    /* Your docs routes go here */ 
    this.route('usage');
  });
});
```

Because Octane no longer has the application-template-wrapper,
the `tests/dummy/app/templates/application.hbs` must be wrapped with
```hbs
<div class='ember-view'>
  <!-- the original content of this file -->
  {{docs-header}}

  {{outlet}}

  {{docs-keyboard-shortcuts}}
</div>
```

Now, to add a header and list:
in `tests/dummy/app/templates/index.hbs`, replace
```hbs
<div style="max-width: 40rem; margin: 0 auto; padding: 0 1.5rem">
  {{#docs-demo as |demo|}}
    {{#demo.example name="my-demo.hbs"}}
      <p>Make sure to read up on the DocsDemo component before building out this page.</p>
    {{/demo.example}}
  {{/docs-demo}}
</div>
```
(yes, I read up on DocsDemo, https://ember-learn.github.io/ember-cli-addon-docs/docs/api/components/docs-demo, but there is next to no information on it, and it doesn't seem to be relevant for just having non-demo / static content? idk.)
with
```hbs

<div class="docs-container docs-md docs-my-16">
  <section class="docs-section docs-max-w-md docs-mx-auto docs-pb-8">
    <h2>h2</h2>

    <p>
      paragraph text
      <ul>
        <li>item 1</li>
        <li>item 2</li>
        <li>item 3</li>
      </ul>
    </p>

    <div class="docs-my-5 docs-text-right">
      {{#docs-link "docs"}}
        <button
          type="button"
          class="docs-bg-grey-darkest docs-text-white docs-py-2 docs-px-4 docs-no-underline docs-rounded hover:docs-bg-black"
        >
          Get started &rarr;
        </button>
      {{/docs-link}}
    </div>
  </section>
</div>
```
where did I get this structure / classes from? here: https://github.com/alexdiliberto/ember-transformicons/blob/master/tests/dummy/app/templates/index.hbs#L4
and the h2 looks correct https://alexdiliberto.com/ember-transformicons/
