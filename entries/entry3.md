Entry 3:

# Working with d3.js
Throughout these past two weeks I have begun tinkering with a few examples provided by the d3.js lexample library.
Now I am sure that the project that wish to do is an iamge circle map, or something similar to it.
While most of the work will be done in html, d3 is used to bring the elements of css alive to look more appealing on
the front end. Javascript is an already difficult language to code in, especially when someone tries to change a tags elements
such as this chunk of code:  
```Js
var paragraphs = document.getElementsByTagName("p");
for (var i = 0; i < paragraphs.length; i++) {
  var paragraph = paragraphs.item(i);
  paragraph.style.setProperty("color", "white", null);
}
```
And turn it into this single line of code:
 ```Js 
 d3.selectAll("p").style("color", "white"); 
 ```
 The line of code above changes all p tags to the color white, as does the longer version above this, but that is more time 
 consuming for the programmer.

 # Tinkering experience 
 After searching for inpsiration on what to base my project on, I found the image circle map.
 As said in before, Image circle maps start out as one huge circle then as the mouse scrolls over it it becomes smaller and 
 divides into more circles of different colors until making an image out of circle! After searching through
 several websites, most of which were graphs, but very well done, I found the image circle map and started looking 
 at its code after playing with it first. when i saw the code that was used in it I felt overwhelmed at first, but
 I decided to use some pieces of codes to determine how they affect the program, while most of it is still somewhat
 complicated I have a grasp on what some pieces of the code do and why there are in their current positions
 For reference, here is an example of the user's image.js file:
 ```Js
  	//PlayMode
            	if(c.classed('notHovered')){
                        c.classed('Hovered',true);
                        if(d3.mouse(this)[0] > t_x)
                        {
                          if(d3.mouse(this)[1] < t_y){

                            c.transition().duration(10)
                                .attr('r',r_)
                                .attr('cx',t_x+(r_))
                                .attr('cy',t_y-(r_))
                                .each("end",function(){
                                  setTimeout(obj.renderCircle(t_x-(r_),t_y-(r_),r_,t_x,t_y,true),0);
                                  setTimeout(obj.renderCircle(t_x-(r_),t_y+(r_),r_,t_x,t_y,true),0);
                                  setTimeout(obj.renderCircle(t_x+(r_),t_y+(r_),r_,t_x,t_y,true),0);
                                });
                          }else{

                            c.transition().duration(10)
                                .attr('r',r_)
                                .attr('cx',t_x+(r_))
                                .attr('cy',t_y+(r_))
                                .each('end',function(){
                                  setTimeout(obj.renderCircle(t_x-(r_),t_y-(r_),r_,t_x,t_y,true),0);
                                  setTimeout(obj.renderCircle(t_x-(r_),t_y+(r_),r_,t_x,t_y,true),0);
                                  setTimeout(obj.renderCircle(t_x+(r_),t_y-(r_),r_,t_x,t_y,true),0);
                                });
                          }
                        }else{
                          if(d3.mouse(this)[1] < t_y){
                            c.transition().duration(10)
                                .attr('r',r_)
                                .attr('cx',t_x-(r_))
                                .attr('cy',t_y-(r_))
                                .each('end',function(){
                                  setTimeout(obj.renderCircle(t_x+(r_),t_y-(r_),r_,t_x,t_y,true),0);
                                  setTimeout(obj.renderCircle(t_x-(r_),t_y+(r_),r_,t_x,t_y,true),0);
                                  setTimeout(obj.renderCircle(t_x+(r_),t_y+(r_),r_,t_x,t_y,true),0);
                                });
                          }else{
                            c.transition().duration(10)
                                .attr('r',r_)
                                .attr('cx',t_x-(r_))
                                .attr('cy',t_y+(r_))
                                .each('end',function(){
                                  setTimeout(obj.renderCircle(t_x-(r_),t_y-(r_),r_,t_x,t_y,true),0);
                                  setTimeout(obj.renderCircle(t_x+(r_),t_y-(r_),r_,t_x,t_y,true),0);
                                  setTimeout(obj.renderCircle(t_x+(r_),t_y+(r_),r_,t_x,t_y,true),0);
                                });                           
                          }
                        }
                      }
            	}
		};
		obj.renderCircle = function(x,y,r,p_x,p_y,v){
			var pixelData = canvas.getContext('2d').getImageData(parseInt(x), parseInt(y), 1, 1).data;

			setTimeout(function(){

      	    	circle = container.select('.cg')
      	    				.append('circle')
        	            	.attr('cx',x)
	            	        .attr('cy',y)
	            	        .attr('r',r)
	                	    //.attr('shape-rendering','auto')
	                    	.style('fill',function() {                      
	                      		return 'rgb('+pixelData[0]+','+pixelData[1]+','+pixelData[2]+')';
	                    	})
	                    	.style('stroke',function() {
	                      		return 'rgb('+pixelData[0]+','+pixelData[1]+','+pixelData[2]+')';
	                    	})
	                    	.attr('class','Hovered');

	                	if(mode==='play'){
	                    		circle.on('mouseover',function(){
	                    				if(mode=='play')
	                    					obj.breakCircle.bind(this)();
		                    			})
		                    			.on('mouseout',function(d){
		                    				if(mode=='play'){
		                    					d3.select(this).classed('Hovered',false);
			                      				d3.select(this).classed('notHovered',true);
		                    				}			                      
			                    		});
	                    	}
	        		},0);
	                    	
	                    	
	            return;

		};
		obj.height = function(_){
			if(!arguments.length) return height;
			height = _;
			return obj;
		};
		obj.width = function(_){
			if(!arguments.length) return width;
			width = _;
			return obj;
		};
		obj.imageName = function(_){
			if(!arguments.length) return imageName;
			imageName = _;
			return obj;
		};
		obj.setMode = function(_){
			if(!arguments.length) return setMode;
			mode = _;
			return obj;
		};
		obj.setImageSize = function(_){
			if(!arguments.length) return size;
			size = _;
			return obj;
		};

	return obj;
	}
})()
 ```
While it may seem daunting at first, I've studied this large chunk of code long enough that this is what makes the playable part of the image map work
By seeing the keywords such as mouseover or Hovered and notHovered it is easily seen that this is for the user part 
to pay with.
 It might take some more time to fully learn how to program something this complicated with d3, but I know i can do it!
 
 ## Takeaways:
 * Break each piece of code part by part, at first I had no idea what all of this meant but then
 I took it slower and examined each piece slowly and started understanding
* Talk with a friend or an object, I found it very useful when trying to figure out which piece did what
so don't be afraid to talk it out with someone even if they might not understand half of this stuff
because both of you will learn as well!