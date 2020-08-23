## BFS模版
                                void bfs(TreeNode root) {
                                                Queue<TreeNode> queue = new ArrayDeque<>();
                                                queue.add(root);
                                                while (!queue.isEmpty()) {
                                                    TreeNode node = queue.poll(); // Java 的 pop 写作 poll()
                                                    if (node.left != null) {
                                                        queue.add(node.left);
                                                    }
                                                    if (node.right != null) {
                                                        queue.add(node.right);
                                                    }
                                                }
                                            }
