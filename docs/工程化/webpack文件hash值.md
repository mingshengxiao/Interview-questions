### webpack 有几种 hash，它们有什么区别？一般你在项目里面是用哪种 hash？

hash：全局 hash。是整个项目的 hash 值，其根据每次编译内容计算得到，每次编译之后都会生成新的 hash,即修改任何文件都会导致所有文件的 hash 发生改变。

chunkHash：分组 hash。根据不同的入口文件(Entry)进行依赖文件解析、构建对应的 chunk，生成对应的哈希值（来源于同一个 chunk，则 hash 值就一样）。当某个入口文件修改后重新打包，会导致本入口文件关联的所有文件的 hash 值都修改，但是不会影响到其他入口文件的 hash 值。

contentHash：内容 hash。根据文件内容生成 hash 值，文件内容相同 hash 值就相同。当规则为 contenthash 时，每个文件的 hash 值都是根据自身内容而生成，当某个文件内容修改时，打包后只会修改其本身的 hash 值，不会影响其他文件的 hash 值。
