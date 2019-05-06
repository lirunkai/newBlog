DOM相关的

## Node

许多 DOM API 对象的类型会从这个接口继承, 比如

`Document Element Attr DocumentFragment DocumentType Notation`

属性(readonly)

`Node.baseURI`  

baseURL表示协议和域名,以及一直到最后一个'/'之前的文件目录

当浏览器要获取绝对 URL 时，就需要用基 URL 去解析相对 URL

`<base href="">` 指定用于一个文档中包含的所有相对 URL 的根 URL

`Node.childNodes` 包含了该节点所有子节点的实时的`NodeList`, 如果该节点的子节点发生了变化, `NodeList`对象就会自动更新

`Node.firstChild`  该节点的第一个子节点

`Node.lastChild` 该节点的最后一个子节点

`Node.isConnected` 返回一个布尔值用来检测该节点是否已连接到一个上下文对象上，DOM连接到`Document`上, `shadow DOM` 连接到`ShadowDom`上

`Node.nextSibling` 返回与该节点同级的下一个节点

`Node.previousSibling` 返回当前同辈节点的前一个节点

`Node.nodeName` 返回一个包含该节点名字的DOMString

`Node.nodeType` 返回一个与该节点类型对应的`无符号短整型`的值

| Name                   | Value |
| ---------------------- | :---: |
| ELEMENT_NODE           |   1   |
| ATTRIBUTE_NODE         |   2   |
| TEXT_NODE              |   3   |
| CDATA_SECTION_NODE     |   4   |
| COMMENT_NODE           |   8   |
| DOCUMENT_NODE          |   9   |
| DOCUMENT_TYPE_NODE     |  10   |
| DOCUMENT_FRAGMENT_NODE |  11   |

`Node.ownerDocument` 返回这个元素属于的Document对象

`Node.parentNode` 返回一个当前节点的Node父节点

`Node.parentElement` 返回一个当前节点的Element父节点

可修改

`Node.textContent` 返回或者设置一个元素内所有子节点及其后代的文本内容

`Node.nodeValue` 返回或设置当前节点的值。

方法

`Node.appendChild(child)` 将一个节点添加到指定父节点的子节点列表末尾。

`Node.cloneNode(deep)` 返回调用该方法的节点的一个副本. 如果deep为true, 子级节点也会被复制

`Node.compareDocumentPosition(otherNode)` 可以比较当前节点与任意文档中的另一个节点的位置关系

| value | des                 |
| ----- | ------------------- |
| 1     | 不在同一文档中      |
| 2     | otherNode在node之前 |
| 4     | otherNode在node之后 |
| 8     | otherNode包含node   |
| 16    | otherNode被node包含 |
| 32    | 待定                |

`Node.contains(otherNode) ` 返回的是一个布尔值，来表示传入的节点是否为该节点的后代节点。

`Node.getRootNode()` 返回上下文的根节点

`Node.hasChildNodes()` 返回一个Boolean,表明当前节点是否包含子节点

`Node.insertBefore(newNode, referenceNode)` 在参考节点之前插入一个拥有指定父节点的子节点

`Node.removeChild()` 移除一个node

`Node.replaceChild(newChild, oldChild)` 用指定的节点替换当前节点的一个子节点，并返回被替换掉的节点。

