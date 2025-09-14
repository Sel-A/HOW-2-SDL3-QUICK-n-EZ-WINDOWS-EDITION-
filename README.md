# HOW-2-SDL3-QUICK-n-EZ-WINDOWS-EDITION-
## WHAT IS THIS????
This is a quick and sleezy, nice and breezy SDL3 tutorial. My OS is Windows 11 (Desktop Version) and the SDL version I'm using is 3.2.20, so I apologize incase anything updates and coders are confused.

## ANYTHING IMPORTANT TO KNOW BEFOREHAND?
Please note that I'm not trying to be all nitty gritty and exacting with a bunch of numbers and so on, I'm going for more of an informal and straight forward tutorial here so I do apologize (again) if you don't get what you're looking for here or have any problems. There will always be the wiki (https://wiki.libsdl.org/SDL3/FrontPage) and youtube AND reddit AND stackoverflow, so I guess try there? Also this is for c/c++. Idk, just felt I needed to say that incase people use other languages for SDL.

## ANYTHING ELSE?
At the time I'm writing this, SDL3 is still somewhat knew so please do have some patience and maybe even try to experiement with SDL2 as it has been significantly more explored by the SDL community and could be a much better pick for you.

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

## WHAT ABOUT SDL3 ITSELF???????
Go to the releases page for SDL3 (https://github.com/libsdl-org/SDL/releases), and lay your eyes upon the plethora of options to (not) choose from. Each of these are designed specifically for certain computer archtecitures, systems, and or methods of use, but for this tutorial I just used "SDL3-devel-3.2.22-mingw.tar.gz", which was at the bottom so you should probably go for something along those lines (look for "devel" and "ming.tar.gz") if you want to follow along with some of the set up. From here, unpack your zip file and beeline it to the "bin" file, or the binary file which is basically the precompiled and already put together version of SDL you can snag, located somewhere at "SDL3\SDL3-3.2.20\x86_64-w64-mingw32\bin". PLEASE REMEMBER WHERE THIS BINARY FILE IS/ITS DIRECTORY, AND KEEP IT THERE/PUT IT IN A SAFER PLACE WHERE YOU WON'T MOVE IT. 

From here, look up something called "environment variables" in your computer before selecting and going into it it, double click/select and edit "path", and add in a new environment variable, typing/copy and pasting the directory of the previously mentioned binary file. With this, there are two things to note: You have have made this binary file accessable in most places in your computer by providing it its directory. However, if you move SDL or need to install a newer version of it, you will need to do all of this over again. This is why I said to keep it in a safe place with and to not really touch it, since shuffling this binary file around throughout the span of a couple folders in the middle of compiling your SDL programs would cause a lot of needless environment variable adjustments. This should be familiar with you since you would probably have needed to do this exact process with GCC. If your using something like clang, its probably the same aswell, but I'll have to look into it (I will in fact, not look into it). But yeah, it should be ready to use now, so please move onto the next section called:
# HOW TO SDL3 QUICK N EZ YO!
## HOW TO COMPILE
DESC. ON HOW: compile with g++, take source code and output to an executable file/directory, include 64 bit include folder from SDL3, link 64 libraries from SDL3, and link the binary file to the project
TERMINAL COMM: g++ "C:\Users\USER1\SOL\Desktop\boidsMain.cpp" -o "C:\Users\USER1\SOL\Desktop\boids.exe" -I "C:\User Downloaded Files\SDL3\SDL3-3.2.20\x86_64-w64-mingw32\include" -L "C:\User Downloaded Files\SDL3\SDL3-3.2.20\x86_64-w64-mingw32\lib" -lSDL3


-----HOW TO INCLUDE IN PROJECT
---First, make sure the sld3's bin (Or binary file) is in window's PATH directory so you can use it where ever you want  
then, "#include <SDL3/SDL.h>" and go ham

-----SET UP/THE PROJECT ITSELF
---Before you do anything, make sure you understand the sdl designated defines functions that will be used before, during and after your program begins to actually run

"#define SDL_MAIN_USE_CALLBACKS" will resolve any entry point issues between SDL3 and your OS n whatnot 

"SDL_AppResult SDL_AppInit(void **appstate, int argc, char *argv[]){}" is the function your progrgam will run once before the main loop where the cool stuff happens. use this for any initiailzation and to "SDL_Init(SDL_INIT_VIDEO)". Without this boolean returning setup, you will get absoloutely no grpahics whatsoever so make sure this sets up 

"SDL_AppResult SDL_AppEvent(void *appstate, SDL_Event *event){
	//if we quit the window
	if (event->type == SDL_EVENT_QUIT){
		//nothing went wrong leading up to this, celebrate
		return SDL_APP_SUCCESS;
	}
	//we dont care abt other events, continue
	return SDL_APP_CONTINUE;
}" beyond basic simulations, this is literally all you need lmao. this checks for any window based events, which to an extent is important but really isnt so thats why i gave all the code needed for it in c++

"SDL_AppResult SDL_AppIterate(void *appstate){}" is the heart and soul of your sdl3 program, acting as the main loop of it all to make pretty pixels move

"void SDL_AppQuit(void *appstate, SDL_AppResult result){}" is like the setup function, but it runs once at the end. used for cleanup so its relavant and kinda important

---notice how most of these return an SDL_AppResult. these are basically values that help determine whether to terminate the program or not, and whether the program actually ran properly

returning "SDL_APP_CONTINUE" in some of these functions just tells sdl3 that everything is running smoothly, and to continue as business permits

returning "SDL_APP_SUCCESS" or "SDL_APP_FAILURE" however, tells sdl3 to terminate the program because it either was a success or failed. pretty straight forward. 

---examples: with the SDL_AppEvent copy and paste we already covered two of the SDL_AppResult values through demonstration, so now we're going to demonstrate the usage of "SDL_APP_FAILURE" in addition to "SDL_Init(SDL_INIT_VIDEO)", since we have mentioned the great importance of making sure this sets up properly before and feel that a proper example is needed to effectively check if setup is done correctly and you can blame your problems on something else

"
//runs once upon startup
SDL_AppResult SDL_AppInit(void **appstate, int argc, char *argv[]){
	//failure init no visuals very bad
	if (!SDL_Init(SDL_INIT_VIDEO)){
		printf("VIDEO FAILURE");
		return SDL_APP_FAILURE;
	}
	//setup was success, continue
	return SDL_APP_CONTINUE;
}
"


-----ACTUALLY DRAWING PIXELS ON YOUR WINDOW
---Get familiar with the SDL_Window and SDL_Renderer data sctructures, these will be responsible for holding your window's information and drawing to your window 

Actually setting up these parts are relatively simple, contrary to how important they are: "SDL_CreateWindowAndRenderer(NAME, WIDTH, HEIGHT, FLAGS, &WINDOW, &RENDERER);"

for a quick rundown, name is the name you give your application which you could view at the top left of your application window, width and height are the dimensions of your window, flags are special and specified properties you want for the window (just put a zero if you dont want any of that, itll still run fine), and window and renderer are the references to your window and renderer. PLEASE NOTE: window and renderer are pointers by themself in this example, making &window and &renderer double pointers if thats what you call them.

here, its also important to check for any nullptrs before continuign on, since without them you wont see squat

---From here, you just need to put forward a little bit more of effort before you have any results, namely with your pixels. SDL_FPoint is your guy here (He holds point information for your pixels), and to work better with the declared functions for him, you need to make him into a pointer (SDL_FPoint*) so he can hold an array full of of pixel infomation. Dont forget to actually give him points though, thats pretty important. Each point will have an x and y variable assigned to it, so give it some random float value between 0 and 1 (noninclusive of 1 :[ ) using SDL_randF() 

Now with that out of the way, there is about 5 lines of code between you and your pixels:
"
SDL_SetRenderDrawColor(RENDERER, r,g,b,a);
SDL_RenderClear(RENDERER);
SDL_SetRenderDrawColor(RENDERER, r,g,b,a);
SDL_RenderPoints(RENDERER, PIXELDATA, PIXELCOUNT);
"
and what these do are also pretty straightfoward, SDL_SetRenderDrawColor() sets the render color to a certain RGBA value, with said value components listed in the following paramters, SDL_RenderClear() wipes your screen clear and sets it to the renderer's current color, and SDL_RenderPoints() takes in your pixel data (your baby girl SDL_FPoint*) and the amount of pixels there are in your data. With this in your main loop, try to compile everythhign and pray to god you havent messed anything up before now to see your pixels.
