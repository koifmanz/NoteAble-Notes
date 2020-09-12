# NoteAble-Notes

## About

Noteable is markdown editor, who is great for note taking, especially together with github for cloud sync.
One great feature of Noteable is the notes organization, which in form of notebooks. 

*Some of Noteable features*:

* You can write KaTeX expressions, Mermaid diagrams and more
* Notes and attachments are simply stored on your disk
* Zen mode and dark theme
* A multi-note editor
* A split-editor

## The Notes

The notes here are collection of things I learn at work or courses, and they varied from GIS, databases to airflow. Most of the notes include a code example or set of steps.

### example for a note:

#### Create Minimal circle

use the following code in geom gen
```python
if(
  area($geometry)/area(minimal_circle($geometry, 100))>0.67,
  minimal_circle($geometry, 100)
  null
)
```

<p align="center">
  <img src="https://pbs.twimg.com/media/ER86y_tWoAIQV21?format=jpg&name=medium" width="700">
</p>

*Code Source: [Twitter: @klaskarlsson](https://twitter.com/klaskarlsson/status/1233769749240336385/photo/1)*

#### Good looking hillshade

1. hillshade above dem
2. style dem:
    * pesudocolor
    * color ramp -> create new color ramp -> cpt-city
    * select topography -> ramp cd-a or sd-a
3. expand min/max value and set it to min/max values
4. set accuracy to actual (slower)
5. select hillshade
6. set blending (under layer rendering) to multiply

*Recipe Source: discover QGIS 3.x, Kurt Menke, chpater 2 Exercice 7.*
