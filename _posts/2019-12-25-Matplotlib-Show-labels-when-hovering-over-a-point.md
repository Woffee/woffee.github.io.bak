---
layout: post
title:  "Matplotlib: Show labels when hovering over a point"
date:   2019-12-25 14:51:18 +0800
categories: notes
---

![Demo](/images/2019/002.jpg)

This code is modified based on [here](https://stackoverflow.com/questions/7908636/possible-to-make-labels-appear-when-hovering-over-a-point-in-matplotlib)

```python

import matplotlib.pyplot as plt

class My_show():
    def __init__(self, points, labels, colors):
        x = points[:, 0]
        y = points[:, 1]
        self.names = labels

        self.c = colors

        self.norm = plt.Normalize(1, 4)
        self.cmap = plt.cm.RdYlGn

        self.fig, self.ax = plt.subplots()
        self.sc = plt.scatter(x, y, c=self.c, s=100, cmap=self.cmap, norm=self.norm)

        self.annot = self.ax.annotate("", xy=(0, 0), xytext=(20, 20), textcoords="offset points",
                            bbox=dict(boxstyle="round", fc="w"),
                            arrowprops=dict(arrowstyle="->"))
        self.annot.set_visible(False)

    def update_annot(self, ind):
        pos = self.sc.get_offsets()[ind["ind"][0]]
        self.annot.xy = pos
        # text = "{}, {}".format(" ".join(list(map(str,ind["ind"]))),
        #                        " ".join([self.names[n] for n in ind["ind"]]))
        text = " ".join([self.names[n] for n in ind["ind"]])

        self.annot.set_text(text)
        self.annot.get_bbox_patch().set_facecolor(self.cmap(self.norm(self.c[ind["ind"][0]])))
        self.annot.get_bbox_patch().set_alpha(0.8)

    def hover(self, event):
        vis = self.annot.get_visible()
        if event.inaxes == self.ax:
            cont, ind = self.sc.contains(event)
            if cont:
                self.update_annot(ind)
                self.annot.set_visible(True)
                self.fig.canvas.draw_idle()
            else:
                if vis:
                    self.annot.set_visible(False)
                    self.fig.canvas.draw_idle()

    def show(self):
        self.fig.canvas.mpl_connect("motion_notify_event", self.hover)
        plt.show()

if __name__ == '__main__':
    my = My_show(points, labels, colors)
    my.show()

```