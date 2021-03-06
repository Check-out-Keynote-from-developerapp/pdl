
### domain: DOM

This domain exposes DOM read/write operations. Each DOM Node is represented with its mirror object
that has an `id`. This `id` can be used to get additional information on the Node, resolve it into
the JavaScript object wrapper, etc. It is important that client receives DOM events only for the
nodes that are known to the client. Backend keeps track of the nodes that were sent to the client
and never sends the same node twice. It is client's responsibility to collect information about
the nodes that were sent to the client.<p>Note that `iframe` owner elements will return
corresponding document elements as their child nodes.</p>

---


#### command: DOM.collectClassNamesFromSubtree 🌱

Collects class names for the node with given id and all of it's child nodes.

*parameters*
-  `nodeId` <[DOM.NodeId]> Id of the node to collect class names

*returns*
-  `classNames` <array of [string]> Class name list

---


#### command: DOM.copyTo 🌱

Creates a deep copy of the specified node and places it into the target container before the
given anchor.

*parameters*
-  `nodeId` <[DOM.NodeId]> Id of the node to copy
-  `targetNodeId` <[DOM.NodeId]> Id of the element to drop the copy into
- *optional* `insertBeforeNodeId` <[DOM.NodeId]> Drop the copy before this node (if absent, the copy becomes the last child of
`targetNodeId`)

*returns*
-  `nodeId` <[DOM.NodeId]> Id of the node clone

---


#### command: DOM.describeNode

Describes node given its id, does not require domain to be enabled. Does not start tracking any
objects, can be used for automation.

*parameters*
- *optional* `nodeId` <[DOM.NodeId]> Identifier of the node
- *optional* `backendNodeId` <[DOM.BackendNodeId]> Identifier of the backend node
- *optional* `objectId` <[Runtime.RemoteObjectId]> JavaScript object id of the node wrapper
- *optional* `depth` <[integer]> The maximum depth at which children should be retrieved, defaults to 1. Use -1 for the
entire subtree or provide an integer larger than 0
- *optional* `pierce` <[boolean]> Whether or not iframes and shadow roots should be traversed when returning the subtree
(default is false)

*returns*
-  `node` <[DOM.Node]> Node description

---


#### command: DOM.disable

Disables DOM agent for the given page.

---


#### command: DOM.discardSearchResults 🌱

Discards search results from the session with the given id. `getSearchResults` should no longer
be called for that search.

*parameters*
-  `searchId` <[string]> Unique search session identifier

---


#### command: DOM.enable

Enables DOM agent for the given page.

---


#### command: DOM.focus

Focuses the given element.

*parameters*
- *optional* `nodeId` <[DOM.NodeId]> Identifier of the node
- *optional* `backendNodeId` <[DOM.BackendNodeId]> Identifier of the backend node
- *optional* `objectId` <[Runtime.RemoteObjectId]> JavaScript object id of the node wrapper

---


#### command: DOM.getAttributes

Returns attributes for the specified node.

*parameters*
-  `nodeId` <[DOM.NodeId]> Id of the node to retrieve attibutes for

*returns*
-  `attributes` <array of [string]> An interleaved array of node attribute names and values

---


#### command: DOM.getBoxModel

Returns boxes for the given node.

*parameters*
- *optional* `nodeId` <[DOM.NodeId]> Identifier of the node
- *optional* `backendNodeId` <[DOM.BackendNodeId]> Identifier of the backend node
- *optional* `objectId` <[Runtime.RemoteObjectId]> JavaScript object id of the node wrapper

*returns*
-  `model` <[DOM.BoxModel]> Box model for the node

---


#### command: DOM.getDocument

Returns the root DOM node (and optionally the subtree) to the caller.

*parameters*
- *optional* `depth` <[integer]> The maximum depth at which children should be retrieved, defaults to 1. Use -1 for the
entire subtree or provide an integer larger than 0
- *optional* `pierce` <[boolean]> Whether or not iframes and shadow roots should be traversed when returning the subtree
(default is false)

*returns*
-  `root` <[DOM.Node]> Resulting node

---


#### command: DOM.getFlattenedDocument

Returns the root DOM node (and optionally the subtree) to the caller.

*parameters*
- *optional* `depth` <[integer]> The maximum depth at which children should be retrieved, defaults to 1. Use -1 for the
entire subtree or provide an integer larger than 0
- *optional* `pierce` <[boolean]> Whether or not iframes and shadow roots should be traversed when returning the subtree
(default is false)

*returns*
-  `nodes` <array of [DOM.Node]> Resulting node

---


#### command: DOM.getNodeForLocation 🌱

Returns node id at given location.

*parameters*
-  `x` <[integer]> X coordinate
-  `y` <[integer]> Y coordinate
- *optional* `includeUserAgentShadowDOM` <[boolean]> False to skip to the nearest non-UA shadow root ancestor (default: false)

*returns*
-  `nodeId` <[DOM.NodeId]> Id of the node at given coordinates

---


#### command: DOM.getOuterHTML

Returns node's HTML markup.

*parameters*
- *optional* `nodeId` <[DOM.NodeId]> Identifier of the node
- *optional* `backendNodeId` <[DOM.BackendNodeId]> Identifier of the backend node
- *optional* `objectId` <[Runtime.RemoteObjectId]> JavaScript object id of the node wrapper

*returns*
-  `outerHTML` <[string]> Outer HTML markup

---


#### command: DOM.getRelayoutBoundary 🌱

Returns the id of the nearest ancestor that is a relayout boundary.

*parameters*
-  `nodeId` <[DOM.NodeId]> Id of the node

*returns*
-  `nodeId` <[DOM.NodeId]> Relayout boundary node id for the given node

---


#### command: DOM.getSearchResults 🌱

Returns search results from given `fromIndex` to given `toIndex` from the search with the given
identifier.

*parameters*
-  `searchId` <[string]> Unique search session identifier
-  `fromIndex` <[integer]> Start index of the search result to be returned
-  `toIndex` <[integer]> End index of the search result to be returned

*returns*
-  `nodeIds` <array of [DOM.NodeId]> Ids of the search result nodes

---


#### command: DOM.hideHighlight

Hides any highlight.

---


#### command: DOM.highlightNode

Highlights DOM node.

---


#### command: DOM.highlightRect

Highlights given rectangle.

---


#### command: DOM.markUndoableState 🌱

Marks last undoable state.

---


#### command: DOM.moveTo

Moves node into the new container, places it before the given anchor.

*parameters*
-  `nodeId` <[DOM.NodeId]> Id of the node to move
-  `targetNodeId` <[DOM.NodeId]> Id of the element to drop the moved node into
- *optional* `insertBeforeNodeId` <[DOM.NodeId]> Drop node before this one (if absent, the moved node becomes the last child of
`targetNodeId`)

*returns*
-  `nodeId` <[DOM.NodeId]> New id of the moved node

---


#### command: DOM.performSearch 🌱

Searches for a given string in the DOM tree. Use `getSearchResults` to access search results or
`cancelSearch` to end this search session.

*parameters*
-  `query` <[string]> Plain text or query selector or XPath search query
- *optional* `includeUserAgentShadowDOM` <[boolean]> True to search in user agent shadow DOM

*returns*
-  `searchId` <[string]> Unique search session identifier
-  `resultCount` <[integer]> Number of search results

---


#### command: DOM.pushNodeByPathToFrontend 🌱

Requests that the node is sent to the caller given its path. // FIXME, use XPath

*parameters*
-  `path` <[string]> Path to node in the proprietary format

*returns*
-  `nodeId` <[DOM.NodeId]> Id of the node for given path

---


#### command: DOM.pushNodesByBackendIdsToFrontend 🌱

Requests that a batch of nodes is sent to the caller given their backend node ids.

*parameters*
-  `backendNodeIds` <array of [DOM.BackendNodeId]> The array of backend node ids

*returns*
-  `nodeIds` <array of [DOM.NodeId]> The array of ids of pushed nodes that correspond to the backend ids specified in
backendNodeIds

---


#### command: DOM.querySelector

Executes `querySelector` on a given node.

*parameters*
-  `nodeId` <[DOM.NodeId]> Id of the node to query upon
-  `selector` <[string]> Selector string

*returns*
-  `nodeId` <[DOM.NodeId]> Query selector result

---


#### command: DOM.querySelectorAll

Executes `querySelectorAll` on a given node.

*parameters*
-  `nodeId` <[DOM.NodeId]> Id of the node to query upon
-  `selector` <[string]> Selector string

*returns*
-  `nodeIds` <array of [DOM.NodeId]> Query selector result

---


#### command: DOM.redo 🌱

Re-does the last undone action.

---


#### command: DOM.removeAttribute

Removes attribute with given name from an element with given id.

*parameters*
-  `nodeId` <[DOM.NodeId]> Id of the element to remove attribute from
-  `name` <[string]> Name of the attribute to remove

---


#### command: DOM.removeNode

Removes node with given id.

*parameters*
-  `nodeId` <[DOM.NodeId]> Id of the node to remove

---


#### command: DOM.requestChildNodes

Requests that children of the node with given id are returned to the caller in form of
`setChildNodes` events where not only immediate children are retrieved, but all children down to
the specified depth.

*parameters*
-  `nodeId` <[DOM.NodeId]> Id of the node to get children for
- *optional* `depth` <[integer]> The maximum depth at which children should be retrieved, defaults to 1. Use -1 for the
entire subtree or provide an integer larger than 0
- *optional* `pierce` <[boolean]> Whether or not iframes and shadow roots should be traversed when returning the sub-tree
(default is false)

---


#### command: DOM.requestNode

Requests that the node is sent to the caller given the JavaScript node object reference. All
nodes that form the path from the node to the root are also sent to the client as a series of
`setChildNodes` notifications.

*parameters*
-  `objectId` <[Runtime.RemoteObjectId]> JavaScript object id to convert into node

*returns*
-  `nodeId` <[DOM.NodeId]> Node id for given object

---


#### command: DOM.resolveNode

Resolves the JavaScript node object for a given NodeId or BackendNodeId.

*parameters*
- *optional* `nodeId` <[DOM.NodeId]> Id of the node to resolve
- *optional* `backendNodeId` <[DOM.BackendNodeId]> Backend identifier of the node to resolve
- *optional* `objectGroup` <[string]> Symbolic group name that can be used to release multiple objects

*returns*
-  `object` <[Runtime.RemoteObject]> JavaScript object wrapper for given node

---


#### command: DOM.setAttributeValue

Sets attribute for an element with given id.

*parameters*
-  `nodeId` <[DOM.NodeId]> Id of the element to set attribute for
-  `name` <[string]> Attribute name
-  `value` <[string]> Attribute value

---


#### command: DOM.setAttributesAsText

Sets attributes on element with given id. This method is useful when user edits some existing
attribute value and types in several attribute name/value pairs.

*parameters*
-  `nodeId` <[DOM.NodeId]> Id of the element to set attributes for
-  `text` <[string]> Text with a number of attributes. Will parse this text using HTML parser
- *optional* `name` <[string]> Attribute name to replace with new attributes derived from text in case text parsed
successfully

---


#### command: DOM.setFileInputFiles

Sets files for the given file input element.

*parameters*
-  `files` <array of [string]> Array of file paths to set
- *optional* `nodeId` <[DOM.NodeId]> Identifier of the node
- *optional* `backendNodeId` <[DOM.BackendNodeId]> Identifier of the backend node
- *optional* `objectId` <[Runtime.RemoteObjectId]> JavaScript object id of the node wrapper

---


#### command: DOM.setInspectedNode 🌱

Enables console to refer to the node with given id via $x (see Command Line API for more details
$x functions).

*parameters*
-  `nodeId` <[DOM.NodeId]> DOM node id to be accessible by means of $x command line API

---


#### command: DOM.setNodeName

Sets node name for a node with given id.

*parameters*
-  `nodeId` <[DOM.NodeId]> Id of the node to set name for
-  `name` <[string]> New node's name

*returns*
-  `nodeId` <[DOM.NodeId]> New node's id

---


#### command: DOM.setNodeValue

Sets node value for a node with given id.

*parameters*
-  `nodeId` <[DOM.NodeId]> Id of the node to set value for
-  `value` <[string]> New node's value

---


#### command: DOM.setOuterHTML

Sets node HTML markup, returns new node id.

*parameters*
-  `nodeId` <[DOM.NodeId]> Id of the node to set markup for
-  `outerHTML` <[string]> Outer HTML markup to set

---


#### command: DOM.undo 🌱

Undoes the last performed action.

---


#### event: DOM.attributeModified

Fired when `Element`'s attribute is modified.

*parameters*
-  `nodeId` <[DOM.NodeId]> Id of the node that has changed
-  `name` <[string]> Attribute name
-  `value` <[string]> Attribute value

---


#### event: DOM.attributeRemoved

Fired when `Element`'s attribute is removed.

*parameters*
-  `nodeId` <[DOM.NodeId]> Id of the node that has changed
-  `name` <[string]> A ttribute name

---


#### event: DOM.characterDataModified

Mirrors `DOMCharacterDataModified` event.

*parameters*
-  `nodeId` <[DOM.NodeId]> Id of the node that has changed
-  `characterData` <[string]> New text value

---


#### event: DOM.childNodeCountUpdated

Fired when `Container`'s child node count has changed.

*parameters*
-  `nodeId` <[DOM.NodeId]> Id of the node that has changed
-  `childNodeCount` <[integer]> New node count

---


#### event: DOM.childNodeInserted

Mirrors `DOMNodeInserted` event.

*parameters*
-  `parentNodeId` <[DOM.NodeId]> Id of the node that has changed
-  `previousNodeId` <[DOM.NodeId]> If of the previous siblint
-  `node` <[DOM.Node]> Inserted node data

---


#### event: DOM.childNodeRemoved

Mirrors `DOMNodeRemoved` event.

*parameters*
-  `parentNodeId` <[DOM.NodeId]> Parent id
-  `nodeId` <[DOM.NodeId]> Id of the node that has been removed

---


#### event: DOM.distributedNodesUpdated 🌱

Called when distrubution is changed.

*parameters*
-  `insertionPointId` <[DOM.NodeId]> Insertion point where distrubuted nodes were updated
-  `distributedNodes` <array of [DOM.BackendNode]> Distributed nodes for given insertion point

---


#### event: DOM.documentUpdated

Fired when `Document` has been totally updated. Node ids are no longer valid.

---


#### event: DOM.inlineStyleInvalidated 🌱

Fired when `Element`'s inline style is modified via a CSS property modification.

*parameters*
-  `nodeIds` <array of [DOM.NodeId]> Ids of the nodes for which the inline styles have been invalidated

---


#### event: DOM.pseudoElementAdded 🌱

Called when a pseudo element is added to an element.

*parameters*
-  `parentId` <[DOM.NodeId]> Pseudo element's parent element id
-  `pseudoElement` <[DOM.Node]> The added pseudo element

---


#### event: DOM.pseudoElementRemoved 🌱

Called when a pseudo element is removed from an element.

*parameters*
-  `parentId` <[DOM.NodeId]> Pseudo element's parent element id
-  `pseudoElementId` <[DOM.NodeId]> The removed pseudo element id

---


#### event: DOM.setChildNodes

Fired when backend wants to provide client with the missing DOM structure. This happens upon
most of the calls requesting node ids.

*parameters*
-  `parentId` <[DOM.NodeId]> Parent node id to populate with children
-  `nodes` <array of [DOM.Node]> Child nodes array

---


#### event: DOM.shadowRootPopped 🌱

Called when shadow root is popped from the element.

*parameters*
-  `hostId` <[DOM.NodeId]> Host element id
-  `rootId` <[DOM.NodeId]> Shadow root id

---


#### event: DOM.shadowRootPushed 🌱

Called when shadow root is pushed into the element.

*parameters*
-  `hostId` <[DOM.NodeId]> Host element id
-  `root` <[DOM.Node]> Shadow root

---


#### type: DOM.NodeId

Unique DOM node identifier.

*base type*
- **integer**

*accepted by command*
- [DOM.collectClassNamesFromSubtree]
- [DOM.copyTo]
- [DOM.describeNode]
- [DOM.focus]
- [CSS.forcePseudoState]
- [DOM.getAttributes]
- [CSS.getBackgroundColors]
- [DOM.getBoxModel]
- [CSS.getComputedStyleForNode]
- [Overlay.getHighlightObjectForTest]
- [CSS.getInlineStylesForNode]
- [CSS.getMatchedStylesForNode]
- [DOM.getOuterHTML]
- [Accessibility.getPartialAXTree]
- [CSS.getPlatformFontsForNode]
- [DOM.getRelayoutBoundary]
- [Overlay.highlightNode]
- [DOM.moveTo]
- [DOM.querySelector]
- [DOM.querySelectorAll]
- [DOM.removeAttribute]
- [DOMDebugger.removeDOMBreakpoint]
- [DOM.removeNode]
- [DOM.requestChildNodes]
- [DOM.resolveNode]
- [DOM.setAttributeValue]
- [DOM.setAttributesAsText]
- [DOMDebugger.setDOMBreakpoint]
- [CSS.setEffectivePropertyValueForNode]
- [DOM.setFileInputFiles]
- [DOM.setInspectedNode]
- [DOM.setNodeName]
- [DOM.setNodeValue]
- [DOM.setOuterHTML]

*property of type*
- [DOM.Node]

*returned from command*
- [DOM.copyTo]
- [DOM.getNodeForLocation]
- [DOM.getRelayoutBoundary]
- [DOM.getSearchResults]
- [DOM.moveTo]
- [DOM.pushNodeByPathToFrontend]
- [DOM.pushNodesByBackendIdsToFrontend]
- [DOM.querySelector]
- [DOM.querySelectorAll]
- [DOM.requestNode]
- [DOM.setNodeName]

*parameter in event*
- [DOM.attributeModified]
- [DOM.attributeRemoved]
- [DOM.characterDataModified]
- [DOM.childNodeCountUpdated]
- [DOM.childNodeInserted]
- [DOM.childNodeRemoved]
- [DOM.distributedNodesUpdated]
- [DOM.inlineStyleInvalidated]
- [Overlay.nodeHighlightRequested]
- [DOM.pseudoElementAdded]
- [DOM.pseudoElementRemoved]
- [DOM.setChildNodes]
- [DOM.shadowRootPopped]
- [DOM.shadowRootPushed]

---


#### type: DOM.BackendNodeId

Unique DOM node identifier used to reference a node that may not have been pushed to the
front-end.

*base type*
- **integer**

*property of type*
- [Accessibility.AXNode]
- [Accessibility.AXRelatedNode]
- [Animation.AnimationEffect]
- [DOM.BackendNode]
- [CSS.CSSStyleSheetHeader]
- [DOMSnapshot.DOMNode]
- [DOMDebugger.EventListener]
- [LayerTree.Layer]
- [DOM.Node]

*accepted by command*
- [DOM.describeNode]
- [DOM.focus]
- [DOM.getBoxModel]
- [DOM.getOuterHTML]
- [Overlay.highlightNode]
- [DOM.pushNodesByBackendIdsToFrontend]
- [DOM.resolveNode]
- [DOM.setFileInputFiles]

*parameter in event*
- [Overlay.inspectNodeRequested]

---


#### type: DOM.BackendNode

Backend node with a friendly name.

*base type*
- **object**

*properties*
-  `nodeType` <[integer]> `Node`'s nodeType
-  `nodeName` <[string]> `Node`'s nodeName
-  `backendNodeId` <[DOM.BackendNodeId]> 

*property of type*
- [DOM.Node]

*parameter in event*
- [DOM.distributedNodesUpdated]

---


#### type: DOM.PseudoType

Pseudo element type.

*base type*
- **string**

*property of type*
- [DOMSnapshot.DOMNode]
- [DOM.Node]
- [CSS.PseudoElementMatches]

---


#### type: DOM.ShadowRootType

Shadow root type.

*base type*
- **string**

*property of type*
- [DOM.Node]

---


#### type: DOM.Node

DOM interaction is implemented in terms of mirror objects that represent the actual DOM nodes.
DOMNode is a base node mirror type.

*base type*
- **object**

*properties*
-  `nodeId` <[DOM.NodeId]> Node identifier that is passed into the rest of the DOM messages as the `nodeId`. Backend
will only push node with given `id` once. It is aware of all requested nodes and will only
fire DOM events for nodes known to the client
- *optional* `parentId` <[DOM.NodeId]> The id of the parent node if any
-  `backendNodeId` <[DOM.BackendNodeId]> The BackendNodeId for this node
-  `nodeType` <[integer]> `Node`'s nodeType
-  `nodeName` <[string]> `Node`'s nodeName
-  `localName` <[string]> `Node`'s localName
-  `nodeValue` <[string]> `Node`'s nodeValue
- *optional* `childNodeCount` <[integer]> Child count for `Container` nodes
- *optional* `children` <array of [DOM.Node]> Child nodes of this node when requested with children
- *optional* `attributes` <array of [string]> Attributes of the `Element` node in the form of flat array `[name1, value1, name2, value2]`
- *optional* `documentURL` <[string]> Document URL that `Document` or `FrameOwner` node points to
- *optional* `baseURL` <[string]> Base URL that `Document` or `FrameOwner` node uses for URL completion
- *optional* `publicId` <[string]> `DocumentType`'s publicId
- *optional* `systemId` <[string]> `DocumentType`'s systemId
- *optional* `internalSubset` <[string]> `DocumentType`'s internalSubset
- *optional* `xmlVersion` <[string]> `Document`'s XML version in case of XML documents
- *optional* `name` <[string]> `Attr`'s name
- *optional* `value` <[string]> `Attr`'s value
- *optional* `pseudoType` <[DOM.PseudoType]> Pseudo element type for this node
- *optional* `shadowRootType` <[DOM.ShadowRootType]> Shadow root type
- *optional* `frameId` <[Page.FrameId]> Frame ID for frame owner elements
- *optional* `contentDocument` <[DOM.Node]> Content document for frame owner elements
- *optional* `shadowRoots` <array of [DOM.Node]> Shadow root list for given element host
- *optional* `templateContent` <[DOM.Node]> Content document fragment for template elements
- *optional* `pseudoElements` <array of [DOM.Node]> Pseudo elements associated with this node
- *optional* `importedDocument` <[DOM.Node]> Import document for the HTMLImport links
- *optional* `distributedNodes` <array of [DOM.BackendNode]> Distributed nodes for given insertion point
- *optional* `isSVG` <[boolean]> Whether the node is SVG

*property of type*
- [DOM.Node]

*returned from command*
- [DOM.describeNode]
- [DOM.getDocument]
- [DOM.getFlattenedDocument]

*parameter in event*
- [DOM.childNodeInserted]
- [DOM.pseudoElementAdded]
- [DOM.setChildNodes]
- [DOM.shadowRootPushed]

---


#### type: DOM.RGBA

A structure holding an RGBA color.

*base type*
- **object**

*properties*
-  `r` <[integer]> The red component, in the [0-255] range
-  `g` <[integer]> The green component, in the [0-255] range
-  `b` <[integer]> The blue component, in the [0-255] range
- *optional* `a` <[number]> The alpha component, in the [0-1] range (default: 1)

*accepted by command*
- [Overlay.highlightFrame]
- [Overlay.highlightQuad]
- [Overlay.highlightRect]
- [Emulation.setDefaultBackgroundColorOverride]

*property of type*
- [Overlay.HighlightConfig]

---


#### type: DOM.Quad

An array of quad vertices, x immediately followed by y for each point, points clock-wise.

*base type*
- **array**

*property of type*
- [DOM.BoxModel]
- [DOM.ShapeOutsideInfo]

*accepted by command*
- [Overlay.highlightQuad]

---


#### type: DOM.BoxModel

Box model.

*base type*
- **object**

*properties*
-  `content` <[DOM.Quad]> Content box
-  `padding` <[DOM.Quad]> Padding box
-  `border` <[DOM.Quad]> Border box
-  `margin` <[DOM.Quad]> Margin box
-  `width` <[integer]> Node width
-  `height` <[integer]> Node height
- *optional* `shapeOutside` <[DOM.ShapeOutsideInfo]> Shape outside coordinates

*returned from command*
- [DOM.getBoxModel]

---


#### type: DOM.ShapeOutsideInfo

CSS Shape Outside details.

*base type*
- **object**

*properties*
-  `bounds` <[DOM.Quad]> Shape bounds
-  `shape` <array of [any]> Shape coordinate details
-  `marginShape` <array of [any]> Margin shape bounds

*property of type*
- [DOM.BoxModel]

---


#### type: DOM.Rect

Rectangle.

*base type*
- **object**

*properties*
-  `x` <[number]> X coordinate
-  `y` <[number]> Y coordinate
-  `width` <[number]> Rectangle width
-  `height` <[number]> Rectangle height

*property of type*
- [DOMSnapshot.InlineTextBox]
- [DOMSnapshot.LayoutTreeNode]
- [LayerTree.ScrollRect]
- [LayerTree.StickyPositionConstraint]

*accepted by command*
- [LayerTree.profileSnapshot]

*parameter in event*
- [LayerTree.layerPainted]

*returned from command*
- [Page.getLayoutMetrics]

[DOM.collectClassNamesFromSubtree]: dom.md#command-domcollectclassnamesfromsubtree "DOM.collectClassNamesFromSubtree"
[DOM.copyTo]: dom.md#command-domcopyto "DOM.copyTo"
[DOM.describeNode]: dom.md#command-domdescribenode "DOM.describeNode"
[DOM.focus]: dom.md#command-domfocus "DOM.focus"
[CSS.forcePseudoState]: css.md#command-cssforcepseudostate "CSS.forcePseudoState"
[DOM.getAttributes]: dom.md#command-domgetattributes "DOM.getAttributes"
[CSS.getBackgroundColors]: css.md#command-cssgetbackgroundcolors "CSS.getBackgroundColors"
[DOM.getBoxModel]: dom.md#command-domgetboxmodel "DOM.getBoxModel"
[CSS.getComputedStyleForNode]: css.md#command-cssgetcomputedstylefornode "CSS.getComputedStyleForNode"
[Overlay.getHighlightObjectForTest]: overlay.md#command-overlaygethighlightobjectfortest "Overlay.getHighlightObjectForTest"
[CSS.getInlineStylesForNode]: css.md#command-cssgetinlinestylesfornode "CSS.getInlineStylesForNode"
[CSS.getMatchedStylesForNode]: css.md#command-cssgetmatchedstylesfornode "CSS.getMatchedStylesForNode"
[DOM.getOuterHTML]: dom.md#command-domgetouterhtml "DOM.getOuterHTML"
[Accessibility.getPartialAXTree]: accessibility.md#command-accessibilitygetpartialaxtree "Accessibility.getPartialAXTree"
[CSS.getPlatformFontsForNode]: css.md#command-cssgetplatformfontsfornode "CSS.getPlatformFontsForNode"
[DOM.getRelayoutBoundary]: dom.md#command-domgetrelayoutboundary "DOM.getRelayoutBoundary"
[Overlay.highlightNode]: overlay.md#command-overlayhighlightnode "Overlay.highlightNode"
[DOM.moveTo]: dom.md#command-dommoveto "DOM.moveTo"
[DOM.querySelector]: dom.md#command-domqueryselector "DOM.querySelector"
[DOM.querySelectorAll]: dom.md#command-domqueryselectorall "DOM.querySelectorAll"
[DOM.removeAttribute]: dom.md#command-domremoveattribute "DOM.removeAttribute"
[DOMDebugger.removeDOMBreakpoint]: domdebugger.md#command-domdebuggerremovedombreakpoint "DOMDebugger.removeDOMBreakpoint"
[DOM.removeNode]: dom.md#command-domremovenode "DOM.removeNode"
[DOM.requestChildNodes]: dom.md#command-domrequestchildnodes "DOM.requestChildNodes"
[DOM.resolveNode]: dom.md#command-domresolvenode "DOM.resolveNode"
[DOM.setAttributeValue]: dom.md#command-domsetattributevalue "DOM.setAttributeValue"
[DOM.setAttributesAsText]: dom.md#command-domsetattributesastext "DOM.setAttributesAsText"
[DOMDebugger.setDOMBreakpoint]: domdebugger.md#command-domdebuggersetdombreakpoint "DOMDebugger.setDOMBreakpoint"
[CSS.setEffectivePropertyValueForNode]: css.md#command-cssseteffectivepropertyvaluefornode "CSS.setEffectivePropertyValueForNode"
[DOM.setFileInputFiles]: dom.md#command-domsetfileinputfiles "DOM.setFileInputFiles"
[DOM.setInspectedNode]: dom.md#command-domsetinspectednode "DOM.setInspectedNode"
[DOM.setNodeName]: dom.md#command-domsetnodename "DOM.setNodeName"
[DOM.setNodeValue]: dom.md#command-domsetnodevalue "DOM.setNodeValue"
[DOM.setOuterHTML]: dom.md#command-domsetouterhtml "DOM.setOuterHTML"
[DOM.Node]: dom.md#type-domnode "DOM.Node"
[DOM.copyTo]: dom.md#command-domcopyto "DOM.copyTo"
[DOM.getNodeForLocation]: dom.md#command-domgetnodeforlocation "DOM.getNodeForLocation"
[DOM.getRelayoutBoundary]: dom.md#command-domgetrelayoutboundary "DOM.getRelayoutBoundary"
[DOM.getSearchResults]: dom.md#command-domgetsearchresults "DOM.getSearchResults"
[DOM.moveTo]: dom.md#command-dommoveto "DOM.moveTo"
[DOM.pushNodeByPathToFrontend]: dom.md#command-dompushnodebypathtofrontend "DOM.pushNodeByPathToFrontend"
[DOM.pushNodesByBackendIdsToFrontend]: dom.md#command-dompushnodesbybackendidstofrontend "DOM.pushNodesByBackendIdsToFrontend"
[DOM.querySelector]: dom.md#command-domqueryselector "DOM.querySelector"
[DOM.querySelectorAll]: dom.md#command-domqueryselectorall "DOM.querySelectorAll"
[DOM.requestNode]: dom.md#command-domrequestnode "DOM.requestNode"
[DOM.setNodeName]: dom.md#command-domsetnodename "DOM.setNodeName"
[DOM.attributeModified]: dom.md#event-domattributemodified "DOM.attributeModified"
[DOM.attributeRemoved]: dom.md#event-domattributeremoved "DOM.attributeRemoved"
[DOM.characterDataModified]: dom.md#event-domcharacterdatamodified "DOM.characterDataModified"
[DOM.childNodeCountUpdated]: dom.md#event-domchildnodecountupdated "DOM.childNodeCountUpdated"
[DOM.childNodeInserted]: dom.md#event-domchildnodeinserted "DOM.childNodeInserted"
[DOM.childNodeRemoved]: dom.md#event-domchildnoderemoved "DOM.childNodeRemoved"
[DOM.distributedNodesUpdated]: dom.md#event-domdistributednodesupdated "DOM.distributedNodesUpdated"
[DOM.inlineStyleInvalidated]: dom.md#event-dominlinestyleinvalidated "DOM.inlineStyleInvalidated"
[Overlay.nodeHighlightRequested]: overlay.md#event-overlaynodehighlightrequested "Overlay.nodeHighlightRequested"
[DOM.pseudoElementAdded]: dom.md#event-dompseudoelementadded "DOM.pseudoElementAdded"
[DOM.pseudoElementRemoved]: dom.md#event-dompseudoelementremoved "DOM.pseudoElementRemoved"
[DOM.setChildNodes]: dom.md#event-domsetchildnodes "DOM.setChildNodes"
[DOM.shadowRootPopped]: dom.md#event-domshadowrootpopped "DOM.shadowRootPopped"
[DOM.shadowRootPushed]: dom.md#event-domshadowrootpushed "DOM.shadowRootPushed"
[Accessibility.AXNode]: accessibility.md#type-accessibilityaxnode "Accessibility.AXNode"
[Accessibility.AXRelatedNode]: accessibility.md#type-accessibilityaxrelatednode "Accessibility.AXRelatedNode"
[Animation.AnimationEffect]: animation.md#type-animationanimationeffect "Animation.AnimationEffect"
[DOM.BackendNode]: dom.md#type-dombackendnode "DOM.BackendNode"
[CSS.CSSStyleSheetHeader]: css.md#type-csscssstylesheetheader "CSS.CSSStyleSheetHeader"
[DOMSnapshot.DOMNode]: domsnapshot.md#type-domsnapshotdomnode "DOMSnapshot.DOMNode"
[DOMDebugger.EventListener]: domdebugger.md#type-domdebuggereventlistener "DOMDebugger.EventListener"
[LayerTree.Layer]: layertree.md#type-layertreelayer "LayerTree.Layer"
[DOM.Node]: dom.md#type-domnode "DOM.Node"
[DOM.describeNode]: dom.md#command-domdescribenode "DOM.describeNode"
[DOM.focus]: dom.md#command-domfocus "DOM.focus"
[DOM.getBoxModel]: dom.md#command-domgetboxmodel "DOM.getBoxModel"
[DOM.getOuterHTML]: dom.md#command-domgetouterhtml "DOM.getOuterHTML"
[Overlay.highlightNode]: overlay.md#command-overlayhighlightnode "Overlay.highlightNode"
[DOM.pushNodesByBackendIdsToFrontend]: dom.md#command-dompushnodesbybackendidstofrontend "DOM.pushNodesByBackendIdsToFrontend"
[DOM.resolveNode]: dom.md#command-domresolvenode "DOM.resolveNode"
[DOM.setFileInputFiles]: dom.md#command-domsetfileinputfiles "DOM.setFileInputFiles"
[Overlay.inspectNodeRequested]: overlay.md#event-overlayinspectnoderequested "Overlay.inspectNodeRequested"
[DOM.Node]: dom.md#type-domnode "DOM.Node"
[DOM.distributedNodesUpdated]: dom.md#event-domdistributednodesupdated "DOM.distributedNodesUpdated"
[DOMSnapshot.DOMNode]: domsnapshot.md#type-domsnapshotdomnode "DOMSnapshot.DOMNode"
[DOM.Node]: dom.md#type-domnode "DOM.Node"
[CSS.PseudoElementMatches]: css.md#type-csspseudoelementmatches "CSS.PseudoElementMatches"
[DOM.Node]: dom.md#type-domnode "DOM.Node"
[DOM.Node]: dom.md#type-domnode "DOM.Node"
[DOM.describeNode]: dom.md#command-domdescribenode "DOM.describeNode"
[DOM.getDocument]: dom.md#command-domgetdocument "DOM.getDocument"
[DOM.getFlattenedDocument]: dom.md#command-domgetflatteneddocument "DOM.getFlattenedDocument"
[DOM.childNodeInserted]: dom.md#event-domchildnodeinserted "DOM.childNodeInserted"
[DOM.pseudoElementAdded]: dom.md#event-dompseudoelementadded "DOM.pseudoElementAdded"
[DOM.setChildNodes]: dom.md#event-domsetchildnodes "DOM.setChildNodes"
[DOM.shadowRootPushed]: dom.md#event-domshadowrootpushed "DOM.shadowRootPushed"
[Overlay.highlightFrame]: overlay.md#command-overlayhighlightframe "Overlay.highlightFrame"
[Overlay.highlightQuad]: overlay.md#command-overlayhighlightquad "Overlay.highlightQuad"
[Overlay.highlightRect]: overlay.md#command-overlayhighlightrect "Overlay.highlightRect"
[Emulation.setDefaultBackgroundColorOverride]: emulation.md#command-emulationsetdefaultbackgroundcoloroverride "Emulation.setDefaultBackgroundColorOverride"
[Overlay.HighlightConfig]: overlay.md#type-overlayhighlightconfig "Overlay.HighlightConfig"
[DOM.BoxModel]: dom.md#type-domboxmodel "DOM.BoxModel"
[DOM.ShapeOutsideInfo]: dom.md#type-domshapeoutsideinfo "DOM.ShapeOutsideInfo"
[Overlay.highlightQuad]: overlay.md#command-overlayhighlightquad "Overlay.highlightQuad"
[DOM.getBoxModel]: dom.md#command-domgetboxmodel "DOM.getBoxModel"
[DOM.BoxModel]: dom.md#type-domboxmodel "DOM.BoxModel"
[DOMSnapshot.InlineTextBox]: domsnapshot.md#type-domsnapshotinlinetextbox "DOMSnapshot.InlineTextBox"
[DOMSnapshot.LayoutTreeNode]: domsnapshot.md#type-domsnapshotlayouttreenode "DOMSnapshot.LayoutTreeNode"
[LayerTree.ScrollRect]: layertree.md#type-layertreescrollrect "LayerTree.ScrollRect"
[LayerTree.StickyPositionConstraint]: layertree.md#type-layertreestickypositionconstraint "LayerTree.StickyPositionConstraint"
[LayerTree.profileSnapshot]: layertree.md#command-layertreeprofilesnapshot "LayerTree.profileSnapshot"
[LayerTree.layerPainted]: layertree.md#event-layertreelayerpainted "LayerTree.layerPainted"
[Page.getLayoutMetrics]: page.md#command-pagegetlayoutmetrics "Page.getLayoutMetrics"
[DOM.BackendNodeId]: dom.md#type-dombackendnodeid "DOM.BackendNodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.BackendNodeId]: dom.md#type-dombackendnodeid "DOM.BackendNodeId"
[DOM.Node]: dom.md#type-domnode "DOM.Node"
[DOM.PseudoType]: dom.md#type-dompseudotype "DOM.PseudoType"
[DOM.ShadowRootType]: dom.md#type-domshadowroottype "DOM.ShadowRootType"
[Page.FrameId]: page.md#type-pageframeid "Page.FrameId"
[DOM.BackendNode]: dom.md#type-dombackendnode "DOM.BackendNode"
[DOM.Quad]: dom.md#type-domquad "DOM.Quad"
[DOM.ShapeOutsideInfo]: dom.md#type-domshapeoutsideinfo "DOM.ShapeOutsideInfo"
[DOM.Quad]: dom.md#type-domquad "DOM.Quad"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.BackendNodeId]: dom.md#type-dombackendnodeid "DOM.BackendNodeId"
[Runtime.RemoteObjectId]: runtime.md#type-runtimeremoteobjectid "Runtime.RemoteObjectId"
[DOM.Node]: dom.md#type-domnode "DOM.Node"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.BackendNodeId]: dom.md#type-dombackendnodeid "DOM.BackendNodeId"
[Runtime.RemoteObjectId]: runtime.md#type-runtimeremoteobjectid "Runtime.RemoteObjectId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.BackendNodeId]: dom.md#type-dombackendnodeid "DOM.BackendNodeId"
[Runtime.RemoteObjectId]: runtime.md#type-runtimeremoteobjectid "Runtime.RemoteObjectId"
[DOM.BoxModel]: dom.md#type-domboxmodel "DOM.BoxModel"
[DOM.Node]: dom.md#type-domnode "DOM.Node"
[DOM.Node]: dom.md#type-domnode "DOM.Node"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.BackendNodeId]: dom.md#type-dombackendnodeid "DOM.BackendNodeId"
[Runtime.RemoteObjectId]: runtime.md#type-runtimeremoteobjectid "Runtime.RemoteObjectId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.BackendNodeId]: dom.md#type-dombackendnodeid "DOM.BackendNodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[Runtime.RemoteObjectId]: runtime.md#type-runtimeremoteobjectid "Runtime.RemoteObjectId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.BackendNodeId]: dom.md#type-dombackendnodeid "DOM.BackendNodeId"
[Runtime.RemoteObject]: runtime.md#type-runtimeremoteobject "Runtime.RemoteObject"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.BackendNodeId]: dom.md#type-dombackendnodeid "DOM.BackendNodeId"
[Runtime.RemoteObjectId]: runtime.md#type-runtimeremoteobjectid "Runtime.RemoteObjectId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.Node]: dom.md#type-domnode "DOM.Node"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.BackendNode]: dom.md#type-dombackendnode "DOM.BackendNode"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.Node]: dom.md#type-domnode "DOM.Node"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.Node]: dom.md#type-domnode "DOM.Node"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.NodeId]: dom.md#type-domnodeid "DOM.NodeId"
[DOM.Node]: dom.md#type-domnode "DOM.Node"
[boolean]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON "JSON boolean"
[string]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON "JSON string"
[number]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON "JSON number"
[integer]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON "JSON integer"
[object]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON "JSON object"
[any]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON "JSON any"