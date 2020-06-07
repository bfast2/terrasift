var header = {};
var left = {};
var bottom = {};
var right = {};
var maps = {};
var styles = {};
var control = {};
var chart = {};

styles.control = {};
styles.control.panel ={
      position: 'top-center',
      maxWidth: '450px',
      padding: '8px'
    }
styles.chart = {};
styles.chart.panel ={
      position: 'top-center',
      width: '450px',
      padding: '8px',
      maxWidth:'450px',
      minWidth:'450px'
    }
styles.control.label = {
  width: '140px'
}
styles.control.widget = {
  width: '250px'
};
styles.bottomLeft = {
  position: 'bottom-left'
}
styles.bottomRight = {
  position: 'bottom-right'
}
styles.topLeft = {
  position: 'top-left'
}
styles.topRight = {
  position: 'top-right'
}
var start = ui.Panel([ui.Label('Start of History',styles.control.label),//2013
                                   ui.Textbox({placeholder: '2016-01-01', value: '2015-01-01', style: styles.control.widget})],ui.Panel.Layout.flow('horizontal'));
var end = ui.Panel([ui.Label('End of Monitoring',styles.control.label),//2018
                                   ui.Textbox({placeholder: '2017-12-31', value: '2018-12-31', style: styles.control.widget})],ui.Panel.Layout.flow('horizontal'));
var historyEnd = ui.Panel([ui.Label('End of History',styles.control.label),
                           ui.DateSlider({start: start.widgets().get(1).getValue(),
                                            end: end.widgets().get(1).getValue(),
                                          value: '2016-12-31',
                                         period: 1,
                                          style: styles.control.widget})],ui.Panel.Layout.flow('horizontal'));

var monitoringStart = ui.Panel([ui.Label('Start of Monitoring',styles.control.label),
                           ui.DateSlider({start: start.widgets().get(1).getValue(),
                                            end: end.widgets().get(1).getValue(),
                                          value: '2017-01-01',
                                         period: 1,
                                          style: styles.control.widget})],ui.Panel.Layout.flow('horizontal'));

var hoptions = [{"label":'0.25', "value":0.25},{"label":'0.5', "value":0.5},{"label":'1', "value":1}]
var h = ui.Panel([ui.Label('h',styles.control.label),
                  ui.Select({items:hoptions, value:0.25, style:styles.control.widget})],ui.Panel.Layout.flow('horizontal'));
var period = ui.Panel([ui.Label('period',styles.control.label),
                       ui.Slider({min:2 , max: 10, value:10, step:2, style:styles.control.widget})],ui.Panel.Layout.flow('horizontal'));
var alpha = ui.Panel([ui.Label('alpha',styles.control.label),
                      ui.Slider({min:0 , max: 0.05, value:0.05, step:0.001, style:styles.control.widget})],ui.Panel.Layout.flow('horizontal'));
var magnitudeThreshold = ui.Panel([ui.Label('magnitude',styles.control.label),
                                   ui.Textbox({placeholder: 'threshold', value: -0.000000000000000000000000000000121, style: styles.control.widget})],ui.Panel.Layout.flow('horizontal'));
var harmonics = ui.Panel([ui.Label('harmonics',styles.control.label),
                      ui.Slider({min:1 , max: 5, value:1, step:1, style:styles.control.widget})],ui.Panel.Layout.flow('horizontal'));

var updateButtons = {}
updateButtons.left = ui.Button({label:'Update', style:styles.bottomLeft})
updateButtons.right = ui.Button({label:'Update', style:styles.bottomRight})
var downloadLink = {}
downloadLink.left = ui.Label({value: 'Generating download link...', style:styles.bottomLeft})
downloadLink.right = ui.Label({value: 'Generating download link...', style:styles.bottomRight})

var downloadLink30 = {}
downloadLink30.left = ui.Label({value: 'Generating download link...', style:styles.bottomLeft})
downloadLink30.right = ui.Label({value: 'Generating download link...', style:styles.bottomRight})

var layerSelection = {}

layerSelection.left = ui.Panel({
  widgets : [ui.Select({
    placeholder:'Select Layer',
    style : styles.topLeft
  })],
  style : styles.topLeft})

layerSelection.right = ui.Panel({
  widgets : [ui.Select({
    placeholder:'Select Layer',
    style : styles.topRight
  })],
  style : styles.topRight})

var runButton = ui.Button('Update both maps')
var buttons = ui.Panel([runButton],ui.Panel.Layout.flow('horizontal'));
control.panel = ui.Panel({
  widgets: [
    start,
    historyEnd,
    monitoringStart,
    end,
    h,
    period,
    alpha,
    magnitudeThreshold,
    harmonics,
    buttons
    ],
    style: styles.control.panel
})

chart.panel = ui.Panel({
  widgets: [
    ui.Label('Click on the map to inspect the BFAST monitor results')
    ],
    style: styles.chart.panel
})

maps.left = ui.Map();
maps.left.which = 'left';
maps.right = ui.Map();
maps.right.which = 'right';
maps.left.style().set('cursor','crosshair')
maps.right.style().set('cursor','crosshair')
maps.left.add(downloadLink.left);
maps.right.add(downloadLink.right);
maps.left.add(downloadLink30.left);
maps.right.add(downloadLink30.right);
maps.left.add(updateButtons.left);
maps.right.add(updateButtons.right);
maps.left.add(layerSelection.left);
maps.right.add(layerSelection.right);

var mapSwipe = ui.SplitPanel({
  firstPanel: maps.left,
  secondPanel: maps.right,
  wipe: true,
  style: {stretch: 'both'}
});
var mapLinker = ui.Map.Linker([mapSwipe.getFirstPanel(),mapSwipe.getSecondPanel()]);

mapLinker.forEach(function(map,index){map.setCenter(-60.00, -14.33,10)})
var middleRight = ui.SplitPanel({
  firstPanel: ui.Panel([mapSwipe]),
  secondPanel: chart.panel,
  wipe: false,
  style: {stretch: 'both'}
})

var middle = ui.SplitPanel({
  firstPanel: control.panel,
  secondPanel: ui.Panel([middleRight]),
  wipe: false,
  style: {stretch: 'both',position:'middle-right'}
})

header = ui.Panel({
  widgets : [
      ui.Label({
        value: 'forest Watchdog',
        style: {fontSize: '20px', fontWeight: 'bold', backgroundColor:"darkgreen", color: 'white'}
      })
  ],
  style: {backgroundColor:"darkgreen", textAlign:'center'}
}
)

bottom = ui.Panel({
  widgets : [
      ui.Label({
        value: 'Help',
        style: {fontSize: '10px', fontWeight: 'bold', backgroundColor: 'lightgrey'},
        targetUrl: 'https://www.rdocumentation.org/packages/bfast/versions/1.5.7/topics/bfastmonitor'
      })
  ],
  style: {backgroundColor: "lightgrey"}
}
)

var show = function show(){
  ui.root.widgets().reset([])
  ui.root.add(header)
  ui.root.add(middle)
  ui.root.add(bottom)
  ui.root.setLayout(ui.Panel.Layout.flow("vertical",true))
}
maps.controlVisibility = {layerList:false, zoomControl:false, scaleControl:true, mapTypeControl:true, fullscreenControl:false, drawingToolsControl:false}
maps.left.setControlVisibility(maps.controlVisibility)
maps.right.setControlVisibility(maps.controlVisibility)
exports.control = control;
exports.buttons = buttons;
exports.maps = maps;
exports.updateButtons = updateButtons;
exports.layerSelection = layerSelection;
exports.chartPanel = chart.panel;
exports.bottom = bottom;
show()