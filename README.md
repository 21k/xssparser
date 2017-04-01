# xssparser
browser side

```{javascript}
function detect(domStr) {
    var dParser = new DOMParser;
    var dom = dParser.parseFromString(domStr, "text/html");
    return {
        dom: dom,
        all: dom.all,
        bads: [].slice.apply(dom.querySelectorAll("*")).filter((node, index)=> {
            return ([].slice.apply(node.attributes).filter(attr=>attr.nodeName.indexOf("on") == 0).length || node.nodeName == "SCRIPT" || node.nodeName == "A" && ["javascript:", "data:", "blob:", "file:"].indexOf(node.protocol) == 0)
        }).map(node=>{
            return {
                value:node.outerHTML,
                node:node
            }
        })
    }
}

```
