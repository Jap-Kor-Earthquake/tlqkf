$(function(){
  // navigator
  var lnb = $('.nav'),
      header = $('.header'),
      openSubH = 330,
      closeSubH = 108,
      timer,
      delay = 200;
  lnb.on({
    'mouseenter': function(){
      timer = setTimeout(function() {
        header.stop();
        header.animate({"height":openSubH,"border-bottom-width":"1px"});
      }, delay)
    },
    'mouseleave': function(){
      clearTimeout(timer);
      header.stop();
      header.animate({"height":closeSubH,"border-bottom-width":0});
    }
  })

  /* layer_popup */
  var modal= $( "[dataformat='modal']" );
  modal.draggable({
    handle: ".pop_header",
    cursor: "move",
    containment: "parent",
    scroll:false
  });
  modal.find("[role='btn_close']").on('click',function(e){
    e.preventDefault();
    $(this).parents('.overlay').hide();
  });

  /* fileDeco */
  $('[role="fileAdd"]').change(function(){
    var fileAdd = $(this);
    fileAdd.parent('span').prev('[role="filePath"]').val(fileAdd.val());
  });

  // accordion
  $('[role="acc"] > div').accordion({
    header : "h2",
    collapsible: true,
    heightStyle: "content",
    icons: {
      "header": "ui-icon-plus",
      "activeHeader": "ui-icon-minus"
    },
    active: false
  });
  $('[role="acc_sub"] > div').accordion({
    header : "h4",
    collapsible: true,
    heightStyle: "content",
    icons: {
      "header": "ui-icon-plus",
      "activeHeader": "ui-icon-minus"
    },
    active: false
  });
  
  /*calendar*/
  $.datepicker.setDefaults({
   /* buttonImageOnly: true,
    showOn: "both",*/
    changeMonth: true,
    changeYear: true,
    numberOfMonths: 1,
    regional:["ko"]
  });

  $( ".date" ).next('img').on('click',function(){
	  $(this).prev('input').focus();
  });
  $( "[dataformat='datepic']" ).datepicker({
      buttonText: "날짜를 선택해주세요."
    });
  $( "[dataformat='from']" ).datepicker({
    buttonText: "시작날짜를 선택해주세요.",
    onClose: function( selectedDate ) {
      var getName=$(this).attr('name');
      $("input[name='"+ getName +"'].to").datepicker( "option", "minDate", selectedDate );
    }
  });
  $( "[dataformat='to']" ).datepicker({
    buttonText: "종료날짜를 선택해주세요.",
    onClose: function( selectedDate ) {
      var getName=$(this).attr('name');
      $("input[name='"+ getName +"'].from").datepicker( "option", "maxDate", selectedDate );
    }
  });
 

  // slectlist evt
  var selList = $('[role="checklist"]'),
      selBtn = selList.find('input'),
      allBtn = $('[role="all"]');    
      selBtn.each(function(){
  if($(this).prop('checked')) $(this).parent('label').addClass('on');
  });
  selBtn.on('change', function(){
    var sel = $(this),
      selP = sel.parents('ul');
    addOn(sel);
    allEvt(selP);
  });
  allBtn.on('change',function(){
    var all = $(this);
    addOn(all);
  })
  function addOn(sel){
    if(sel[0].type === 'radio'){
      sel.parents('ul').find('label').removeClass('on');
    }
    (sel.prop('checked')) ?
      sel.parents('label').addClass('on') :
      sel.parents('label').removeClass('on');
    }
  function allEvt(selP){
    var checkLeng = selP.find(':checkbox:checked').length,
        allLeng = selP.find(':checkbox').length,
        thisAll = selP.prev('label').find('[role="all"]');
    (checkLeng === allLeng) ?
    thisAll.prop('checked',true).parents('label').addClass('on') :
    thisAll.prop('checked',false).parents('label').removeClass('on');
  }
  allBtn.on('change',function(){
    var sel = $(this),
       selUl = $(this).parent('label').next('ul');
    if(sel.prop('checked')){
      selUl.find(':checkbox').prop('checked',true);
      selUl.find('label').addClass('on');
    }else{
      selUl.find(':checkbox').prop('checked',false);
      selUl.find('label').removeClass('on');
    }
  });
});

// tab
var tab_conts = $('.tab_conts'),
    tab_list = $('.tab_list'), 
    tab_btn = $('.tab_list li');

  tab_conts.find('.tab_cont').hide();
  tab_conts.find('.tab_cont:first').show();
  tab_list.find('li:first').find('a').addClass('on');
  tab_btn.on('click','a', function(e){
    e.preventDefault();
    var getId = $(this).prop('href').split('#')[1];
    $(this).parents('.tab').next('.tab_conts').find('.tab_cont').hide();
    $(this).parents('.tab_list').find('a').removeClass('on');
    $(this).addClass('on');
    $('#'+getId).show();
  });


//데이터 널 공백치환
function dataNull(data){
	if(data==null){
		return "";
	}
	return data;
}

/*******************************************************************
 *  1. 함수명    :  onlyNumber
 *  2. 입력값    :
 *  3. 리턴값    :  event -> true false
 *  4. 내용      :  숫자만 기입받게 하는 방법
 *  5. 특이사항    :  style="ime-mode:disabled"
 ********************************************************************/
function onlyNumber(){
  var mkey = event.keyCode;
  flag = false;
  if((mkey >= 48) && (mkey <= 57) || (mkey >= 96) && (mkey <= 105)){
    //숫자
    flag = true;
  }else if((mkey == 46) || (mkey == 8)){
    //delete, backspace
    flag = true;
  }else if((mkey == 9) || (mkey == 37) || (mkey == 39) || (mkey == 35) || (mkey == 36)){
    //tab, <-, -> , home, end
    flag = true;
  }else if((event.keyCode == 110) || (event.keyCode == 190) || (event.keyCode == 189) || (event.keyCode == 109)){
       //., -
 flag = true;
  }
  event.returnValue=flag;
}

