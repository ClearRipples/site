#动画效果集


---

css3和硬件传感器动画效果集合。

##CSS3动效
  
  <div class="jsmodule-content">
      <ul id="cssCase" class="cwf-list">
      </ul>        
  </div>
  
##使用硬件传感器api

  <div class="js-module-content">
      <ul id="apiCase" class="cwf-list">              
      </ul>        
  </div>

<script id="csscase-template" type="text/x-handlebars-template">
  {{#each csscase}}
    <li>
      <div class="pic">
          <img alt="" src="{{pic}}" width="160" />
      </div>
      <div class="cwfqr" data-url="{{url}}">
        <a href="{{url}}" target="_blank">
        <div class="qr"></div>
        </a>
      </div>
      <div class="desc">
        <div class="tit">{{tit}}</div>
        <div class="author">来自{{author}}</div>
      </div>
    </li>
  {{/each}}
</script>

<script id="apicase-template" type="text/x-handlebars-template">
  {{#each apicase}}
    <li>
      <div class="pic">
          <img alt="" src="{{pic}}" width="160" />
      </div>
      <div class="cwfqr" data-url="{{url}}">
        <a href="{{url}}" target="_blank">
        <div class="qr"></div>
        </a>
      </div>
      <div class="desc">
        <div class="tit">{{tit}}</div>
        <div class="author">来自{{author}}</div>
      </div>
    </li>
  {{/each}}
</script>

<script src="http://frozenui.github.io/static/qrcode.js"></script>

<script type="text/javascript">

  seajs.use(['handlebars'], function(Handlebars) {
    var casedata ={ 
        csscase: [], 
        apicase: []
        };
    var cssTemplate,apiTemplate;

    var jqxhr = $.getJSON("../static/data.json", function(data) {
        casedata.csscase = data.csscase;
        casedata.apicase = data.apicase;
        cssTemplate = Handlebars.compile($("#csscase-template").html());
        apiTemplate = Handlebars.compile($("#apicase-template").html());
    })
    .success(function() {
        $('#cssCase').html(cssTemplate(casedata));
        $('#apiCase').html(apiTemplate(casedata));
    })
    .error(function() { alert("error"); })
    .complete(function() {
        $(".cwfqr").each(function(index,el){
          var url=$(el).attr("data-url");
          $(this).find(".qr").qrcode(url);
        });
    });   
  });
  
</script>
