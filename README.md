# ember-async-expanding-tree
This addon provides a async-expanding-tree component for ember. It's a configurable, recursive component to display a expandable tree. 
Child nodes are fetched asynchronously. 

## Installation
`ember install ember-async-expanding-tree`

## Usage
include the component in your template, you need to provide at least a model

`{{async-expanding-tree model=topNode}}`

specify your own config to customize the functionality of the tree:

`{{async-expanding-tree model=topNode config=customConfig}}`

```
  config:
    # property path to the property that should be used as label
    # e.g. model.label.en would be label.en
    labelPropertyPath: 'label'
    # function that is called with the selected model when the label of the model is clicked
    onActivate: (model) ->
    # function to retrieve children of the parent object
    # this function should return a Promise that resolves with the children of the given model 
    # as Ember Models.
    getChildren: (model) ->
      model.reload()
    # list of concept ids that are expanded
    # will auto expand a node in the tree if it's id is cont
    # ained in this array
    expandedConcepts: []
    # max amount (n) of children to be shown before a load more button is presented
    # load more button shows an extra n children
    showMaxChildren: 50
    # show nodes without children
    includeLeafs: true
    # component to be rendered before the tree node
    # model wil be passed to the component
    beforeComponent: null
    # component to be rendered after the tree node
    # model wil be passed to the component
    afterComponent: null
```

if necessary, the component can fetch the children of the model on init
`{{async-expanding-tree model=topNode config=config fetchChildrenOnInit=true}}`

you can also specify tooltips for the node, the expander button, the label or the load more button.
to do this, add one or more of these functions to the config 
```
config:
  getTooltipNode: (level) ->
      if level is 0 then 'first level'
      else then 'other levels'
  getTooltipExpander: (level) ->
      if level is 0 then 'first level'
      else then 'other levels'
  getTooltipLabel: (level) ->
      if level is 0 then 'first level'
      else then 'other levels'
  getTooltipLoadMore: (level) ->
    if level is 0 then 'first level'
    else then 'other levels'
```

you can also specify whether you want the children to display tooltips or whether you want the default values to be used
```
config:
  showChildrenTooltips: false
  showDefaultTooltips: false
```
