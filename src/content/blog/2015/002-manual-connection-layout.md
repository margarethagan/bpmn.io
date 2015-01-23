---

title: Manual connection layout
layout: blogpost.hbs

slug: 2015-manual-connection-layout
author: Jörg Dotzki<https://github.com/ISO50>

published: 2015-01-22 18:00

---


<p class="introduction">
With our first release this year we have added a lot of new features and technical improvements. We improved the connection handling and shipped also a modeler version within our bower package.
</p>

<!-- continue -->

## Modeler
### Connection handling
We added the ability to customize bend points and reconnect connections to different sources / targets.

The user could add new bend points and move them around to control the layout of the connection manually.
To support the user creating clean diagrams, the connection snaps automatically at vertical and horizontal orientation.

<div style="margin: 30px 0; text-align: center">
  <a href="http://demo.bpmn.io/new">
    <img style="box-shadow: 0px 2px 6px 2px #C2C2C2; max-width: 100%"
src="{{ assets }}/attachments/blog/2015/002-bendpoints.gif">
  </a>
</div>

Also the start and end point of a connection can be moved and attached to another shape.

<div style="margin: 30px 0; text-align: center">
  <a href="http://demo.bpmn.io/new">
    <img style="box-shadow: 0px 2px 6px 2px #C2C2C2; max-width: 100%"
  src="{{ assets }}/attachments/blog/2015/002-reconnect.gif">
  </a>
</div>


### Selection

The modeler now support two selection modes. First one is by using our new lasso tool. It allows to draw a box around the elements you want to select.
The other way allows adding individual elements to the selection.

<div style="margin: 30px 0; text-align: center">
  <a href="http://demo.bpmn.io/new">
    <img style="box-shadow: 0px 2px 6px 2px #C2C2C2; max-width: 100%"
  src="{{ assets }}/attachments/blog/2015/002-lasso-tool.gif">
  </a>
</div>

<table>
  <tr>
    <th style="padding-right: 15px">Function</th>
    <th style="padding-right: 15px">Key combination</th>
  </tr>
  <tr>
    <td style="padding-right: 15px">Lasso tool</td>
    <td style="padding-right: 15px">Hold `Alt` key + left mouse button + mouse move</td>
  </tr>
  <tr>
    <td style="padding-right: 15px">Add elements to selection</td>
    <td style="padding-right: 15px">Hold `Shift` key + left mouse</td>
  </tr>
</table>


### Standard Keyboard Shortcuts
We added a more consistent way handling keyboard events. Developers should have a look at the documentation of this new [Keyboard service](https://github.com/bpmn-io/diagram-js/blob/master/lib/features/keyboard/Keyboard.js).


For Mac users the system specific shortcuts were added.

<table>
  <tr>
    <th style="padding-right: 15px">Function</th>
    <th style="padding-right: 15px">Keyboard shortcut</th>
  </tr>
    <td style="padding-right: 15px">Delete</td>
    <td style="padding-right: 15px">`Del`</td>
  <tr>
    <td style="padding-right: 15px">Undo</td>
    <td style="padding-right: 15px">`Strg` + z, `Cmd` + z</td>
  </tr>
  <tr>
    <td style="padding-right: 15px">Redo</td>
    <td style="padding-right: 15px">`Strg` + y, `Cmd` + `shift` + z</td>
  </tr>
</table>


## Technical improvements
### Bower package

The bower package also got an update. We ship now three different versions within the package:

* A simple viewer
* A viewer with mouse navigation capability
* A modeler


Additional changes to previous version:

* The package ships with all necessary css + font files
* The location of artifacts changed from . -> ./dist

To install the package:
```bash
bower install bpmn-js
```


### bpmn-moddle
The modeler supports correct serialization / deserialization of 'di extensions' as defined in the BPMN specification.
See this as an example what is possible:


```xml
<bpmn2:definitions xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:bpmn2="http://www.omg.org/spec/BPMN/20100524/MODEL" xmlns:bpmndi="http://www.omg.org/spec/BPMN/20100524/DI" xmlns:dc="http://www.omg.org/spec/DD/20100524/DC" xmlns:di="http://www.omg.org/spec/DD/20100524/DI" id="Definitions_1" targetNamespace="http://bpmn.io/bpmn">
  <bpmn2:process id="Process_1">
    <bpmn2:task id="Task_1">
      <bpmn2:outgoing>SequenceFlow_1</bpmn2:outgoing>
    </bpmn2:task>
    <bpmn2:sequenceFlow id="SequenceFlow_1" name="" sourceRef="Task_1" targetRef="ParallelGateway_1">
      <bpmn2:conditionExpression xsi:type="bpmn2:tFormalExpression">${foo > bar}</bpmn2:conditionExpression>
    </bpmn2:sequenceFlow>
    <bpmn2:parallelGateway id="ParallelGateway_1">
      <bpmn2:incoming>SequenceFlow_1</bpmn2:incoming>
    </bpmn2:parallelGateway>
  </bpmn2:process>
  <bpmndi:BPMNDiagram id="BPMNDiagram_1">
    <bpmndi:BPMNPlane id="BPMNPlane_1" bpmnElement="Process_1">
      <bpmndi:BPMNShape id="_BPMNShape_Task_4" bpmnElement="Task_1">
        <di:extension xmlns:vendor="http://mycompany">
          <vendor:color>green</vendor:color>
        </di:extension>
        <dc:Bounds height="80.0" width="100.0" x="194.0" y="166.0"/>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="_BPMNShape_ParallelGateway_2" bpmnElement="ParallelGateway_1">
        <dc:Bounds height="50.0" width="50.0" x="504.0" y="180.0"/>
        <bpmndi:BPMNLabel>
          <dc:Bounds height="0.0" width="0.0" x="529.0" y="235.0"/>
        </bpmndi:BPMNLabel>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNEdge id="BPMNEdge_SequenceFlow_1" bpmnElement="SequenceFlow_1" sourceElement="_BPMNShape_Task_4" targetElement="_BPMNShape_ParallelGateway_2">
        <di:waypoint xsi:type="dc:Point" x="294.0" y="206.0"/>
        <di:waypoint xsi:type="dc:Point" x="504.0" y="205.0"/>
        <bpmndi:BPMNLabel>
          <dc:Bounds height="6.0" width="6.0" x="316.0" y="206.0"/>
        </bpmndi:BPMNLabel>
      </bpmndi:BPMNEdge>
    </bpmndi:BPMNPlane>
  </bpmndi:BPMNDiagram>
</bpmn2:definitions>
```
