# Setting up Surge XR on Repl.it

Follow these steps to set up and run the Surge XR application on Repl.it:

1. Create a new Repl:
   - Go to [Repl.it](https://replit.com)
   - Click on "+ Create Repl"
   - Choose "React" as the template
   - Name your Repl (e.g., "SurgeXR")

2. Set up the project structure:
   - In the file explorer, create a new folder called `components`
   - Inside `components`, create a new file called `SurgeXR.js`
   - Copy the entire `SurgeXR` component code into `SurgeXR.js`

3. Install dependencies:
   - In the Shell tab, run the following commands:
     ```
     npm install three @react-three/fiber @react-three/drei
     npm install @radix-ui/react-slider
     ```

4. Create a custom Slider component:
   - In the `components` folder, create a new file called `Slider.js`
   - Add the following code to `Slider.js`:
     ```jsx
     import React from 'react';
     import * as SliderPrimitive from '@radix-ui/react-slider';

     const Slider = React.forwardRef(({ className, ...props }, ref) => (
       <SliderPrimitive.Root
         ref={ref}
         className={`relative flex w-full touch-none select-none items-center ${className}`}
         {...props}
       >
         <SliderPrimitive.Track className="relative h-2 w-full grow overflow-hidden rounded-full bg-secondary">
           <SliderPrimitive.Range className="absolute h-full bg-primary" />
         </SliderPrimitive.Track>
         <SliderPrimitive.Thumb className="block h-5 w-5 rounded-full border-2 border-primary bg-background ring-offset-background transition-colors focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50" />
       </SliderPrimitive.Root>
     ));
     Slider.displayName = SliderPrimitive.Root.displayName;

     export { Slider };
     ```

5. Modify `SurgeXR.js`:
   - Update the import statement for the Slider:
     ```jsx
     import { Slider } from './Slider';
     ```
   - Remove the `mountRef` and directly use `canvas` element
   - Wrap the component with `Canvas` from `@react-three/fiber`
   - Use `useThree` and `useFrame` hooks for scene setup and animation

6. Update `App.js`:
   - Replace the contents of `App.js` with:
     ```jsx
     import './App.css';
     import SurgeXR from './components/SurgeXR';

     function App() {
       return (
         <div className="App">
           <SurgeXR />
         </div>
       );
     }

     export default App;
     ```

7. Add water normal texture:
   - Download a water normal texture (e.g., from [here](https://29a.ch/sandbox/2012/caustics/causticsNormal.jpg))
   - Upload the image to your Repl (drag and drop into the file explorer)
   - Update the texture path in `SurgeXR.js`:
     ```jsx
     waterNormals: new THREE.TextureLoader().load('/causticsNormal.jpg', function (texture) {
       texture.wrapS = texture.wrapT = THREE.RepeatWrapping;
     }),
     ```

8. Run the application:
   - Click the "Run" button at the top of the Repl.it interface

Your Surge XR application should now be running in the Repl.it environment. You can view it in the webview pane on the right side of the Repl.it interface.

Note: Due to the limitations of the Repl.it environment, you might experience some performance issues with the 3D rendering. For optimal performance, consider running the project locally or on a more powerful hosting platform.
