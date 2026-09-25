export function walkTree(e, node, plugins) {
  const promises = [];
  for (const plugin of plugins.flat()) {
    if (plugin.filter(node)) {
      promises.push(plugin.transform(node, e));
    }
  }
  if (!node.props?.children || !Array.isArray(node.props.children))
    return promises;
  if (node.props.children.length === 0) {
    delete node.props.children;
    return promises;
  }
  for (const child of node.props.children || []) {
    if (child && typeof child === "object") {
      promises.push(
        ...walkTree(e, child, plugins)
      );
    }
  }
  return promises;
}
export function defineTransformer(transformer) {
  return transformer;
}
