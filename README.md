# HOW-2-SDL3-QUICK-n-EZ-WINDOWS-EDITION-
## WHAT IS THIS????
This is a quick and sleezy, nice and breezy SDL3 tutorial to draw a few pixels onto your screen. My OS is Windows 11 (Desktop Version) and the SDL version I'm using is 3.2.20, so I apologize incase anything updates and coders are confused.

Ok well, admittantly a 2 to 2 1/2 hundred lines of text and a few paragraphs are a lot to take in, but honestly most of the information needed to draw a bunch of pixels onto your screen is right here, plus I'll even drop you all the code to play around with and use, so really isn't the extra unexpected length just a slight trade off? Whatever, disregarding my deceptive tactics, I'm here to help you and myself when I eventually do forget this, or not idk. Its better to be prepared and have nothing happen, than to be unprepared and have everything happen.

One more thing: I WILL GIVE YOU FULL EXAMPLE CODE WITH COMMENTS AT THE VERY END RIGHT. Please reference the documentation, as there you will find the actual function signatures, additional explanaions, code and what not. 

Wiki: https://wiki.libsdl.org/SDL3/FrontPage 

NOTE: Make sure you're looking at SDL3 documentation, documentation for SDL2 will sometimes pop up and potentially give you misleading information for your current version. Theres a reason why one is named SDL3 and the other is named SDL2, __they're not exactly the same thing.__

## ANY CONCERNS WITH THIS BEFORE I MOVE ON??? 
My favorite household pet is a rabbit. I take neither side on the cat vs dog debate, as I consider the role of the rabbit in house hold pet and center of attention to be well above cats or dogs. Oh yeah and the slight verbosity, if that's even a word.

## no like with the tutorial
oh nah its good, lil wordy tho

its out of neccesity so take what you want from that 

## ANYTHING IMPORTANT TO KNOW BEFOREHAND?
In this guide/tutorial/hold my hand and tell me about this story momma/how-2-ez I'm going for more of an nonprofessional (because informal kinda holds a more negative connotation towards me), forward and yet cautious tutorial here so I do apologize (again) if you don't get what you're looking for here or have any problems. There will always be the wiki (https://wiki.libsdl.org/SDL3/FrontPage) and youtube AND reddit AND stackoverflow, so I guess try there? Also this is for c++. Idk, just felt I needed to say that incase people use other languages for SDL. Never seen it before though.

## ANYTHING ELSE?
At the time I'm writing this, SDL3 is still somewhat new so please do have some patience and maybe even try to experiement with SDL2 as it has been significantly more explored by the SDL community and could be a much better pick for you.

# PREREQUISITES IF THATS HOW YOU SPELL IT
## COMPUTER SPECIFICATIONS YO
If you just bought a new and recently released windows laptop, you should probably be good for computer specifications and what not. But if you're really concerned, any window's desktop version is supposed to work while some other window versions won't. Just Look at some of the wiki stuff: (https://wiki.libsdl.org/SDL3/README-windows). Really, just have a decent laptop and you should be good to go.

## GRAPHICS DRIVERS
Considering SDL is a sort of GRAPHICS LIBRARY (Ermmm, aschtualy its "a cross-platform software development library"), you would probably want to have an up to date graphics driver (The software that lets your computer talk to your graphics card, which in total makes awesome pictures on your screen appear). I personally have and use an Intel graphics driver, but other computers may use NVIDIA or AMD's graphic drivers. 

## INSTALLING SAID DRIVERS
For installing/replacing new Intel graphics drivers look here: https://www.intel.com/content/www/us/en/search.html#sort=%40lastmodifieddt%20descending&f:@tabfilter=[Downloads]&f:@stm_10385_en=[Graphics] 

For NVIDIA: https://www.nvidia.com/en-us/drivers/

For AMD: https://www.amd.com/en/support/download/drivers.html

For other or any difficulties: Google it and youtube it (You probably won't need to watch a video though), it took me little to no time finding these links off of the official websites for these, so I would assume its like this for other graphics drivers aswell. Installing drivers are not too hard either, so youtube it if you want to go completely braindead or you're just scared or uncertain over what you're doing.

## WHAT ABOUT SDL3 ITSELF??????? WHERE DO I GET ME MY SDL???????
Go to the releases page for SDL3 (https://github.com/libsdl-org/SDL/releases), and lay your eyes upon the plethora of options to (not) choose from. Each of these are designed specifically for certain computer archtecitures, systems, and or methods of use, but for this tutorial I just used "SDL3-devel-3.2.22-mingw.tar.gz", which was at the bottom so you should probably go for something along those lines (look for "devel" and "ming.tar.gz") if you want to follow along with some of the set up. From here, unpack your zip file and beeline it to the "bin" file, or the binary file which is basically the precompiled and already put together version of SDL you can snag, located somewhere at "SDL3\SDL3-3.2.20\x86_64-w64-mingw32\bin". PLEASE REMEMBER WHERE THIS BINARY FILE IS/ITS DIRECTORY, AND KEEP IT THERE/PUT IT IN A SAFER PLACE WHERE YOU WON'T MOVE IT. 

From here, look up something called "environment variables" in your computer before selecting and going into it it, double click/select and edit "path", and add in a new environment variable, typing/copy and pasting the directory of the previously mentioned binary file. With this, there are two things to note: You have have made this binary file accessable in most places in your computer by providing it its directory. However, if you move SDL or need to install a newer version of it, you will need to do all of this over again. This is why I said to keep it in a safe place with and to not really touch it, since shuffling this binary file around throughout the span of a couple folders in the middle of compiling your SDL programs would cause a lot of needless environment variable adjustments. This should be familiar with you since you would probably have needed to do this exact process with GCC. If your using something like clang, its probably the same aswell, but I'll have to look into it (I will in fact, not look into it). But yeah, it should be ready to use now, so please move onto the next section called:

# HOW TO SDL3 ~~QUICK~~ at a moderate speed N EZ YO!

## HOW TO INCLUDE IN PROJECT
First, make sure the sld3's bin (Or binary file) is in window's PATH directory so you can use it where ever you want. Afterwards, you're just an include away from using SDL's graphical capabilities:

 	//including SDL3's header file, all full of the cool stuff you definitely want. 
	//Curious of whats actually in it? Go find it in your SDL3 folder and look through it
	#include <SDL3/SDL.h>
	//literally it, go ham budders

## SET UP/THE PROJECT ITSELF
Before doing anything, defining SDL Callbacks will help resolve any entry point issues (Your main function) between SDL3 and your OS if there is any. I'm pretty sure there is with windows, since I definitely needed to the callbacks to get anything to pop up on my screen, so define callbacks BEFORE including SDL3.

	//defined BEFORE including sdl3, otherwise sdl3 won't see your macro for enabling/defining it, thus failing to turn on callbacks
	#define SDL_MAIN_USE_CALLBACKS 1
	#include <SDL3/SDL.h>
	//helps with sdl3 entrypoint/main funtions
 	#include <SDL3/SDL_main.h>


# THE FOUR WISE FUNTCIONS
As of now, we gotta make sure you understand the key SDL functions that will be used before, during and after running your program to actually run within your main file.

SDL App Initialization is the function your program will run once before the main loop where the cool stuff happens. Use this for any kinds of initiailzation, such as initializing the SDL video subsytem, which is directly responsible for, you guessed it, the readying for the visual aspects of your application. 

Actually, make sure to check if the initialization for that, the video subsystem, is actually initialized and returns true as a result, otherwise you won't get any graphics. I apologize for this, but I can't help but emphasize on this and a few more things since the failure of one of component can lead to frustrating debugging sessions since it doesn't exactly always throw an error if something doesn't work. Good checking and security measures are key, such as with the initial check of the video subsystem's state and the print statement that follows to help pin point the location of the error, rather than just being told there is one and scrambling to locate it. 'Nuff yapping, here's the code that was explained in the previous paragraph:

	//Runs once upon program start up
	SDL_AppResult SDL_AppInit(void **appstate, int argc, char *argv[]){
  		//video subsystem to set up check
  		if (!SDL_Init(SDL_INIT_VIDEO)){
			//failure so announce it and die
			printf("VIDEO INIT FAILURE");
   			//we will cover these return statements deeper into the tutorial, 
	  		// lets cover these few important functions first okay?
			return SDL_APP_FAILURE;
		}
  		//move onto the main loop of the program
		return SDL_APP_CONTINUE;
	}

Next on the list of big names is SDL App Iterate, which is the heart of your program. Here is where your graphics come to live and exist before being wiped off the screen. More on that later, somewhere where we talk about drawing pixels. How this function works is relatively simple: Its one big loop. This function runs tons of times per second, and every iteration you get to perform your graphical escapades before finally showing off your masterpiece to your screen. If its not clicking, think of how we're going to use it like normal animation: for every frame (iteration of the loop/function), we pull up a new piece of paper to begin working on (clearing the window), draw what we want (render our pixels), then present to ourselves and get a good look at them (sending our renderered work to the window to actually see) before moving onto the next frame (moving onto the next iteration).

	SDL_AppResult SDL_AppIterate(void *appstate){
		//wipe the screen clean for this drawing
  		//draw the drawing
		//show it off

		//moves on to another step, whether that may be checking for events or ending the program off
		// both of which are actually functions we will cover right now
		return SDL_APP_CONTINUE;
	}

As foreshadowed by the code, we move onto SDL App Event, who is the function responsible for handling any window events that occur. This can include resizing, exiting, and whatever else. To keep it straightforward and encourage your own exploration, I will only be demonstrating how to close out an application using SDL App Event. In my opinion, we have bigger fish to fry than handling window resizing if we're moving through graphics programming.
	
 	SDL_AppResult SDL_AppEvent(void *appstate, SDL_Event *event){
		//quit window check
		if (event->type == SDL_EVENT_QUIT){
			//nothing went wrong leading up to this celebrate
			return SDL_APP_SUCCESS;
		}
		//we dont care abt other events, continue
		return SDL_APP_CONTINUE;
	}

To appropriately end things off with these four core important functions, we end with the SDL App Quit function, which as you could have predicted, runs once when the program is set into motion to end. This guy is the guy you wanna work with if you need to clean up resources that need to be cleaned.

	void SDL_AppQuit(void *appstate, SDL_AppResult result){
 		//cleanup
	}

## WAIT PLEASE WAIT WOAH, WHAT ABOUT THE RETURN STATEMENTS??

Oh yeah those. Ok so to keep things brief yet effective, as you might have already figured out, these returns of type SDL App Result determine the next course of action. SDL Success, Continue, and Failure stop the program out of success, continue the program, and stop the program out of failure out of error. This would probably explain why SDL App Result doesn't have any return types, since it always runs at the end of a program whether it was successful or not before the process eventually ends. (There is no code demonstration, as the return values have already been demonstrated in the four previously discussed functions)


# HOW DO I GET A WINDOW POP TO UP
Get familiar with the SDL Window and SDL Renderer data structures, these will be responsible for holding your window's information and drawing to your window, which if you don't know, is kinda the whole reason your here. Actually setting up these parts are relatively simple, contrary to how important they are. For the renderer, think of it like a brush of sorts for drawing pixels, you'll see why eventually.

	//your window and renderer
 	SDL_Window* window;
  	SDL_Renderer* renderer;
	//the function that sets up said window and renderer
 	SDL_CreateWindowAndRenderer("Application Name 1", 400, 200, 0, &window, &renderer);
	//...
 	return SDL_APP_CONTINUE;
  
For a quick rundown, the function takes a char* const for the name you want for your application, the application window's width and height respectively, any window flags which can be used for some pretty interesting things like automatically setting the window to fullscreen or just flat out minimizing it upon program execution, and of course the memory addresses to your window and renderer pointers. If you're not familiar with double pointers, watch some youtube videos over it and it'll probably get better. All it needs is a little time and everything will make some sense. Do note that it is also important to check for null pointers, as you really can't have an application with visuals without the visuals. But with this continues your journey to your beautious pixels. Don't forget that print statement to help differentiate between errors.

 	//your window and renderer
 	SDL_Window* window;
  	SDL_Renderer* renderer;
    //window dimensions, very slim tall bounds for funsies 
	// (you should 100% change the very slim window you get though)
	int boundsHeight = 50;
	int boundsWidth = 300;
	//the function that IS SUPPOSED TO set up said window and renderer, 
 	// but we double check anyways for security and program functinality like a good programmer
 	if (!SDL_CreateWindowAndRenderer("Application Name 1", boundsWidth, boundsHeight, 0, &window, &renderer)){
		//failure so announce this and die 
  		printf("WINDOW RENDERER CREATE FAILURE");
		return SDL_APP_FAILURE;
  	}
	//...
 	return SDL_APP_CONTINUE;

NOTE: Please do remember to declare window and renderer variables globally, last thing you want to do is make a black screen appear and reflect your sad face back not because you don't like blank screens, but because this was supposed to be more than just a blank screen. Some of these demonstrations may not exactly be the way you want to implement the shown code in your own.


# PIXELS YESSIR 
From here, assuming you did everything else in this tutorial, you just need to put forward a little bit more of effort before you have any results, namely with your pixels. SDL_FPoint is your guy here (He holds point information for your pixels). Dont forget to actually give him points though, thats pretty important. Each point will have an x and y variable assigned to it, so give it some random float value between 0 and 1 (noninclusive of 1) using SDL_randF(). Also make sure your points are globally accessable.

	//your pixels (Pixel count is dependent on how good your computer is, 
 	// but its still going to be able to support a decent amount of pixels
  	// if statements is where performance starts to get ya)
	int pixelCount = 3000;
 	//very slim tall bounds for funsies 
	int boundsHeight = 50;
	int boundsWidth = 300;
	//whole array for your points
	SDL_FPoint* pointData = new SDL_FPoint[pixelCount];
	//giving each of your points random-ish positions
 	for (int i = 0; i < pixelCount; i++){
		//random positions within zero and the given bounds
  		// (points will not have positons either to either of the bound values)
 		pointData[i].x = SDL_randf() * boundsWidth;
 		pointData[i].y = SDL_randf() * boundsHeight; 
	}
  

Now with that out of the way, there is about 5 lines of code between you and your pixels:

	SDL_SetRenderDrawColor(renderer, r,g,b,a);
	SDL_RenderClear(renderer);
	SDL_SetRenderDrawColor(renderer, r,g,b,a);
	SDL_RenderPoints(renderer, pointData, pixelCount);
	SDL_RenderPresent(renderer);

What these do are also pretty straightfoward, SDL_SetRenderDrawColor() sets the render color to a certain RGBA value, with said value components listed in the following paramters, SDL_RenderClear() wipes your screen clear and sets it to the renderer's current color, SDL_RenderPoints() takes in your pixel data (your baby girl SDL_FPoint*) and the amount of pixels there are in your data to draw your pixels onto a buffer (think of it like storing your wet painting somewhere to dry), and SDL_RenderPresent() brings your buffer to the front/onto the window for you to actually see (pulling that painting back out to look when the colors finally set). With this portion of code in your main loop, try to compile everything and pray to god you havent messed anything up before now to see your pixels. As mentioned before, try not to copy and paste everything into your code willy nilly, it may not work in the way you intend for it to work. Please view the example at the very end for the idea on how and where these functions and structures are used. 

# HOW TO COMPILE
I'll make this very quick, assuming you really want some results right about now. Compile with g++, take source code and output to an executable file/directory, include 64 bit include folder from SDL3, link 64 libraries from SDL3, and link the binary file to the project. Heres an example:

	g++ "C:\Users\USER1\SOL\Desktop\boidsMain.cpp" -o "C:\Users\USER1\SOL\Desktop\boids.exe" -I "C:\User Downloaded Files\SDL3\SDL3-3.2.20\x86_64-w64-mingw32\include" -L "C:\User Downloaded Files\SDL3\SDL3-3.2.20\x86_64-w64-mingw32\lib" -lSDL3

Please also note if you haven't figured it out already, that the terminal command's description that I gave goes in order in terms of describing the pieces to this command. Heres a more generalized version:

	g++ "mainFileDirectory" -o "mainExecutableDirectory" -I "SDL3includeFolderDirectory" -L "SDL3includeLibraryrDirectory" -lSDL3

# EXAMPLE CODE
	//g++ "mainFileDirectory" -o "mainExecutableDirectory" -I "SDL3includeFolderDirectory" -L "SDL3includeLibraryrDirectory" -lSDL3
	//defined BEFORE including sdl3, otherwise sdl3 won't see your macro for enabling/defining it, thus failing to turn on callbacks
	#define SDL_MAIN_USE_CALLBACKS 1
	//including SDL3's header file, all full of the cool stuff you definitely want. 
	#include <SDL3/SDL.h>
	//helps with sdl3 entrypoint/main funtions
	#include <SDL3/SDL_main.h>
	//for our printf error reporters
	#include <stdio.h>
	
	//(I indented comments and declarations for nicer lookin code
	// ZERO purpose beyond that tho lol)
	//global/key variables to the program
		//your window and renderer
			SDL_Window* window;
			SDL_Renderer* renderer;
		//your pixels (Pixel count is dependent on how good your computer is, 
	 	// but its still going to be able to support a decent amount of pixels
	  	// if statements is where performance starts to get ya)
			int pixelCount = 3000;
		//very slim tall bounds for funsies 
		// (you should 100% change the very slim window you get though)
			int boundsWidth = 50;
			int boundsHeight = 300;
		//whole array for your point structure
			SDL_FPoint* pointData = new SDL_FPoint[pixelCount];
	
	
	//Runs once upon program start up
	SDL_AppResult SDL_AppInit(void **appstate, int argc, char *argv[]){
		//video subsystem to set up check
		if (!SDL_Init(SDL_INIT_VIDEO)){
			//failure so announce it and die
			printf("VIDEO INIT FAILURE");
			//we will cover these return statements deeper into the tutorial, 
	  		// lets cover these few important functions first okay?
			return SDL_APP_FAILURE;
		}
	
		//the function that IS SUPPOSED TO set up said window and renderer, 
		// but we double check anyways for security and program functinality like a good programmer
	 	if (!SDL_CreateWindowAndRenderer("Application Name 1", boundsWidth, boundsHeight, 0, &window, &renderer)){
		//failure so announce this and die 
			printf("WINDOW RENDERER CREATE FAILURE");
			return SDL_APP_FAILURE;
		}
	
		//giving each of your points random-ish positions
		for (int i = 0; i < pixelCount; i++){
			//random positions within zero and the given bounds
			// (points will not have positons either to either of the bound values)
			pointData[i].x = SDL_randf() * boundsWidth;
			pointData[i].y = SDL_randf() * boundsHeight; 
		}
	
		//move onto the main loop of the program
		return SDL_APP_CONTINUE;
	}
	
	SDL_AppResult SDL_AppIterate(void *appstate){
		//wipe the screen clean for this drawing (setting it to black)
		SDL_SetRenderDrawColor(renderer, 0,0,0,255);
		SDL_RenderClear(renderer);
		
		/*(not really) BONUS CONTENT 
		//!!!!!SEIZURE WARNING OF SORTS!!!!!
		//this gives it a static effect of sorts
		//giving each of your points random-ish positions
		for (int i = 0; i < pixelCount; i++){
			//random positions within zero and the given bounds
			// (points will not have positons either to either of the bound values)
			pointData[i].x = SDL_randf() * boundsWidth;
			pointData[i].y = SDL_randf() * boundsHeight; 
		}
		*/
	
		//draw the drawing (white pixels)
		SDL_SetRenderDrawColor(renderer, 255,255,255,255);
		SDL_RenderPoints(renderer, pointData, pixelCount);
	
		//show it off
		SDL_RenderPresent(renderer);
		
		//moves on to another step, whether that may be checking for events or ending the program off
		// both of which are actually functions we will cover right now
		return SDL_APP_CONTINUE;
	}
	
	SDL_AppResult SDL_AppEvent(void *appstate, SDL_Event *event){
		//quit window check
		if (event->type == SDL_EVENT_QUIT){
			//nothing went wrong leading up to this celebrate
			return SDL_APP_SUCCESS;
		}
		//we dont care abt other events, continue
		return SDL_APP_CONTINUE;
	}
	
	void SDL_AppQuit(void *appstate, SDL_AppResult result){
		//cleanup
  		//ive been told sdl3 does the cleanup for us...
		//dunno bout that, but try to figure out how to destroy
  		//and deinitialize stld3's video subsystem, window and renderer
		//lil "challenge from me"
  		//(HINT: There are literally functions for these)
	}





















Thank you for reading <3
