# How to add [fullpage.js](https://alvarotrigo.com/fullPage) to elementor

##Requirement:
Encorporate fullpage.js to elementor without [Wordpress fullpage.js](https://alvarotrigo.com/fullPage/wordpress-plugin-elementor/).


[Demo Link](http://the-liana.com) We have setup on a site

## How to Add
1. Copy the footer file from parent theme to child theme
2. First create full height sections in elementor the setting is given below

![Add Fullpage Js to Elementor](/screenshot/section-setting-for-elementor-full-page.png)

3. Remove the footer from your theme or re-edit the footer file to remove content.

4. Paste the following code to your footer (or use footer script plugin) to add js to your theme. We recommeneded to add via footer.php so conditions can be added. paste the below code before wp_footer();

```JS
	<script type="text/javascript">
	jQuery(document).ready(function(){
		var myFullpage = new fullpage('.page-wrapper', {
			//Navigation
			menu: '#menu',
			lockAnchors: false,
			//anchors:['one', 'two','three','four'],
			navigation: true,
			navigationPosition: 'right',
			navigationTooltips: [],
			showActiveTooltip: false,
			slidesNavigation: false,
			slidesNavPosition: 'bottom',
			licenseKey: 'gplv3-license',
			credits: { enabled: false, label: '', position: 'right'},
			//Scrolling
			css3: true,
			scrollingSpeed: 700,
			autoScrolling: true,
			fitToSection: true,
			fitToSectionDelay: 1000,
			scrollBar: false,
			easing: 'easeInOutCubic',
			easingcss3: 'ease',
			loopBottom: false,
			loopTop: false,
			loopHorizontal: true,
			continuousVertical: false,
			continuousHorizontal: false,
			scrollHorizontally: false,
			interlockedSlides: false,
			dragAndMove: false,
			offsetSections: false,
			resetSliders: true,
			fadingEffect: false,
			scrollOverflow: false,
			scrollOverflowReset: false,
			scrollOverflowOptions: null,
			touchSensitivity: 15,
			bigSectionsDestination: null,
			//Accessibility
			keyboardScrolling: true,
			animateAnchor: true,
			recordHistory: true,
			//Design
			controlArrows: true,
			verticalCentered: true,
			paddingTop: '',
			paddingBottom: '',
			fixedElements: '#header',
			responsiveWidth: 0,
			responsiveHeight: 0,
			responsiveSlides: false,
			parallax: false,
			parallaxOptions: {type: 'reveal', percentage: 62, property: 'translate'},
			cards: false,
			cardsOptions: {perspective: 100, fadeContent: true, fadeBackground: true},
			//Custom selectors
			//normalScrollElements:'#lastsection',
			sectionSelector: 'section',
			slideSelector: '.slide',
			lazyLoading: true,
			//events
			onLeave: function(origin, destination, direction){},
			afterLoad: function(origin, destination, direction){
				//full_page_color_switch();
				
			},
			afterRender: function(){
				//full_page_color_switch();
			},
			afterResize: function(width, height){},
			afterReBuild: function(){},
			afterResponsive: function(isResponsive){},
			afterSlideLoad: function(section, origin, destination, direction){},
			onSlideLeave: function(section, origin, destination, direction){}
		});
</script>
```

5. There is a line called **fixedElements: '#header',** in the code above
6. Use your fixed element class or id (in my case this is #header
7. Enjoy using fullpage.js in elementor.

### Extras Work 
There is another thing i have done is call back function after load and after render
```JS
function full_page_color_switch(){
	var activeSection = jQuery('.elementor-section.active');
	if(activeSection.length){
		if(activeSection.hasClass('darksection')){
			jQuery('#header').removeClass('makeheaderlight');
			jQuery('#header').removeClass('makeheaderdark');
			jQuery('#fp-nav').removeClass('makenavlight');
			jQuery('#fp-nav').removeClass('makenavdark');
			jQuery('.et_b_header-logo-img').removeClass('makelogodark');
			jQuery('.et_b_header-logo-img').removeClass('makelogolight');
			jQuery('#header').addClass('makeheaderlight');
			jQuery('#fp-nav').addClass('makenavlight');
			jQuery('.et_b_header-logo-img').addClass('makelogolight');
		}
		if(activeSection.hasClass('lightsection')){
			jQuery('#header').removeClass('makeheaderlight');
			jQuery('#header').removeClass('makeheaderdark');
			jQuery('#fp-nav').removeClass('makenavlight');
			jQuery('#fp-nav').removeClass('makenavdark');
			jQuery('.et_b_header-logo-img').removeClass('makelogodark');
			jQuery('.et_b_header-logo-img').removeClass('makelogolight');
			jQuery('#header').addClass('makeheaderdark');
			jQuery('#fp-nav').addClass('makenavdark');
			jQuery('.et_b_header-logo-img').addClass('makelogodark');
		}
	}
}
```
What the above function do is switch the header color scheme according to the class given to the section and also it switch the sidebar navigation bullets.
