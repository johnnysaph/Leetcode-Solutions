class TreeAncestor:

    def _get_children(self, n):
        children = [[] for i in range(n)]
        for i in range(1, n):
            children[self.parents[i]].append(i)
        return children

    def _get_leaves(self, n):
        return [i for i in range(n) if self.children[i] == []]

    def _get_pointers_and_mapping(self, n):
        pointers = [None for i in range(n)]
        mapping = {}
        for l in self.leaves:
            i = 0
            node = l
            parent = self.parents[node]
            start = node
            branch = []
            #print('aaa', node, start, pointers)
            while node != -1:
                if pointers[node] != None:
                    #print('ups')
                    break
                branch.append(node)
                pointers[node] = (start, i)
                i = i + 1
                if parent < 0 or len(self.children[parent]) > 1:
                    #print('ooo', node, branch, start)
                    mapping[start] = (branch, parent)
                    start = parent
                    i = 0
                    branch = []
                node = self.parents[node]
                parent = self.parents[node]
            #print('uuu', node, parent)
        return pointers, mapping

    def __init__(self, n, parent):
        self.parents = parent
        self.children = self._get_children(n)
        self.leaves = self._get_leaves(n)
        self.pointers, self.mapping = self._get_pointers_and_mapping(n)

    def getKthAncestor(self, node, k):
        key, i = self.pointers[node]
        branch, parent = self.mapping[key]
        if i + k >= len(branch):
            k = k - (len(branch) - i - 1)
            i = -1
            while True:
                if parent < 0:
                    return -1
                branch, parent = self.mapping[parent]
                if k <= len(branch):
                    break
                else:
                    k = k - len(branch)
        return branch[i+k]
