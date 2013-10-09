---
layout: post
title: "centerLineInScrollPane"
description: ""
category: 
tags: []
---
{% include JB/setup %}


    public static void centerLineInScrollPane(JTextComponent component) {
        Container container = SwingUtilities.getAncestorOfClass(JViewport.class, component);

        if (container == null) {
            return;
        }

        try {
            Rectangle r = component.modelToView(component.getCaretPosition());
            JViewport viewport = (JViewport) container;

            int extentWidth = viewport.getExtentSize().width;
            int viewWidth = viewport.getViewSize().width;

            int x = Math.max(0, r.x - (extentWidth / 2));
            x = Math.min(x, viewWidth - extentWidth);

            int extentHeight = viewport.getExtentSize().height;
            int viewHeight = viewport.getViewSize().height;

            int y = Math.max(0, r.y - (extentHeight / 2));
            y = Math.min(y, viewHeight - extentHeight);

            viewport.setViewPosition(new Point(x, y));
        } catch (BadLocationException e) {
            Logger.getLogger(mainJFrame.class.getName()).log(Level.SEVERE, null, e);
        }
    }
