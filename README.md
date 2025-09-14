# HOW-2-SDL3-QUICK-n-EZ-WINDOWS-EDITION-
This is a quick and sleezy, nice and breezy SDL3 tutorial. My OS is Windows 11 (Desktop Version) and the SDL version I'm using is 3.2.20, so I apologize incase anything updates and coders are confused.

Please note that I'm not trying to be all nitty gritty and exacting with a bunch of numbers and so on, I'm going for more of an informal and straight forward tutorial here so I do apologize (again) if you don't get what you're looking for here or have any problems. There will always be the wiki (https://wiki.libsdl.org/SDL3/FrontPage) and youtube AND reddit AND stackoverflow, so I guess try there? 

At the time I'm writing this, SDL3 is still somewhat knew so please do have some patience and maybe even try to experiement with SDL2 as it has been significantly more explored by the SDL community and could be a much better pick for you.

# PREREQUISITES IF THATS HOW YOU SPELL IT
If you just bought a new and recently released windows laptop, you should probably be good for computer specifications and what not. But if you're really concerned, any window's desktop version is supposed to work while some other window versions won't. Just Look at some of the wiki stuff: (https://wiki.libsdl.org/SDL3/README-windows). Really, just have a decent laptop and you should be good to go.

Considering SDL is a sort of GRAPHICS LIBRARY ("Ermmm, aschtualy its 'a cross-platform software development library'"), you would probably want to have an up to date graphics driver (The software that lets your computer talk to your graphics card, which in total makes awesome pictures on your screen appear). 

# HOW TO SDL3 QUICK N EZ YO!

-----HOW TO COMPILE
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
