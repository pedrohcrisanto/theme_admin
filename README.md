[WIP] - RailsAdmin Rollincode Theme
--------------------

This theme provide a modern override of default bootstrap 3 rails_admin theme.
Its provides news colors, adjustments and a brand new tree view menu.

![DASHBOARD](http://i.imgur.com/Mtsr0l4.png, "rollincode")

Like we can't include custom js in a bundled theme with raild_admin for now, so, you have to add in your `app/assets/javascripts/rails_admin/custom/ui.js` the following code :
It will make the javascript menu works.

  $(doument).on('ready pjax:success', function() {
    handleActiveBase();
    function handleActiveBase() {
      $('.sub-menu').each(function () {
        if ($(this).hasClass('active')) {
          $(this).parent().prev().addClass('active');
          $(this).parent().prev().addClass('open');
          $(this).parent().slideDown();
        }
      });
    }
  });

  $(function () {
    var width = $('.nav-stacked').width();
    $('.navbar-header').width(width);

    var array_menu = [];
    var lvl_1 = null;
    var count = 0;

    $('.sidebar-nav li').each(function (index, item) {
      if ($(item).hasClass('dropdown-header')) {
        lvl_1 = count++;
        array_menu[lvl_1] = []
      } else {
        $(item).addClass('sub-menu sub-menu-' + lvl_1);
      }
    });

    for (var i = 0; i <= array_menu.length; i++) {
      $('.sub-menu-' + i).wrapAll("<div class='sub-menu-container' />");
    }

    $('.sub-menu-container').hide();

    handleActiveBase();
    function handleActiveBase() {
      $('.sub-menu').each(function () {
        if ($(this).hasClass('active')) {
          $(this).parent().prev().addClass('active');
          $(this).parent().slideDown();
        }
      });
    }

    $('.dropdown-header').bind('click', function () {
      $('.dropdown-header').removeClass('open');
      $(this).addClass('open');

      $('.dropdown-header').removeClass('active');
      $('.sub-menu-container').stop().slideUp();
      $(this).toggleClass('active');
      $(this).next('.sub-menu-container').stop().slideDown();
    });
  });

This project rocks and uses MIT-LICENSE.