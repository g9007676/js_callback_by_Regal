# js_callback_by_Regal

這是公司前輩寫的 callback method (這名詞定義還需要跟資深前輩討論釐清)

先在此做個記錄

# CODE 

    function tabScroll(){
        var LastScroll = 0;
        var NowScroll = 0;
    
        var EndCallBack = (function(){
            var time;
            return function(){
                if(time) clearTimeout(time);
                time = setTimeout(function () {
                    LastScroll = $(window).scrollTop();
                }, 1);
            }
        })();
    
        var Animate = (function(){
    
            var LastType = '';
    
            return function(v){ /*up, down*/
                if (LastType===v) return;
                LastType = v;
                if(v==='up'){
                    $('h1 .tabbar').animate({top:"-50px"},300);
                    $('h1').animate({height:"40px"},300);
                }else if(v==='down'){
                    $('h1 .tabbar').animate({top:"40px"},300);
                    $('h1').animate({height:"100px"},300);
                }
            }
    
        })();
    
    
        $(window).on('scroll.sidebar', function () {
            NowScroll = $(window).scrollTop();
            if(LastScroll >= NowScroll){
                Animate('up');
            }else if (NowScroll <= 30){
                Animate('down');
            } else {
                Animate('down');
            }
    
            EndCallBack();
        });
    }
