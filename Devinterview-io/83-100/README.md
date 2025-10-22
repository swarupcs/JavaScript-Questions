

## 83. What are polyfills, and when would you use them?

A polyfill is a piece of code (usually JavaScript) that provides modern functionality on older browsers that don't natively support it. The term comes from "poly" (many) and "fill" (filling gaps), meaning it "fills in" missing features.

**How Polyfills Work:**

Polyfills detect if a feature is missing and implement it using available functionality:

```javascript
// Example: Array.includes() polyfill
if (!Array.prototype.includes) {
  Array.prototype.includes = function(searchElement, fromIndex) {
    if (this == null) {
      throw new TypeError('"this" is null or not defined');
    }
    
    const O = Object(this);
    const len = O.length >>> 0;
    
    if (len === 0) return false;
    
    const n = fromIndex | 0;
    let k = Math.max(n >= 0 ? n : len - Math.abs(n), 0);
    
    while (k < len) {
      if (O[k] === searchElement) {
        return true;
      }
      k++;
    }
    
    return false;
  };
}

// Now Array.includes() works in all browsers
[1, 2, 3].includes(2); // true
```

**Common Polyfills:**

**1. Promise Polyfill:**

```javascript
// Check if Promise exists
if (typeof Promise === 'undefined') {
  // Load promise polyfill
  window.Promise = (function() {
    // Polyfill implementation
    function Promise(executor) {
      // ... implementation
    }
    
    Promise.prototype.then = function(onFulfilled, onRejected) {
      // ... implementation
    };
    
    Promise.prototype.catch = function(onRejected) {
      return this.then(null, onRejected);
    };
    
    return Promise;
  })();
}

// Or use a library
// npm install promise-polyfill
import 'promise-polyfill/src/polyfill';
```

**2. Fetch Polyfill:**

```javascript
// Check if fetch exists
if (!window.fetch) {
  // Load whatwg-fetch polyfill
  import('whatwg-fetch');
}

// Usage remains the same
fetch('/api/data')
  .then(response => response.json())
  .then(data => console.log(data));
```

**3. Object.assign Polyfill:**

```javascript
if (typeof Object.assign !== 'function') {
  Object.defineProperty(Object, 'assign', {
    value: function assign(target, ...sources) {
      if (target == null) {
        throw new TypeError('Cannot convert undefined or null to object');
      }
      
      const to = Object(target);
      
      for (let index = 0; index < sources.length; index++) {
        const nextSource = sources[index];
        
        if (nextSource != null) {
          for (const nextKey in nextSource) {
            if (Object.prototype.hasOwnProperty.call(nextSource, nextKey)) {
              to[nextKey] = nextSource[nextKey];
            }
          }
        }
      }
      
      return to;
    },
    writable: true,
    configurable: true
  });
}
```

**4. String.prototype Methods:**

```javascript
// String.startsWith()
if (!String.prototype.startsWith) {
  String.prototype.startsWith = function(search, pos) {
    pos = !pos || pos < 0 ? 0 : +pos;
    return this.substring(pos, pos + search.length) === search;
  };
}

// String.endsWith()
if (!String.prototype.endsWith) {
  String.prototype.endsWith = function(search, this_len) {
    if (this_len === undefined || this_len > this.length) {
      this_len = this.length;
    }
    return this.substring(this_len - search.length, this_len) === search;
  };
}

// String.includes()
if (!String.prototype.includes) {
  String.prototype.includes = function(search, start) {
    if (typeof start !== 'number') {
      start = 0;
    }
    
    if (start + search.length > this.length) {
      return false;
    } else {
      return this.indexOf(search, start) !== -1;
    }
  };
}
```

**When to Use Polyfills:**

**1. Supporting Older Browsers:**

```javascript
// Check browser support analytics
// If significant users on IE11 or older browsers
// Load necessary polyfills

// Example: Supporting IE11
if (!window.Promise) {
  require('promise-polyfill/src/polyfill');
}

if (!window.fetch) {
  require('whatwg-fetch');
}

if (!Array.from) {
  require('core-js/features/array/from');
}
```

**2. Using Modern JavaScript Features:**

```javascript
// When using ES6+ features in production
import 'core-js/stable';
import 'regenerator-runtime/runtime';

// Now you can safely use:
const result = [1, 2, 3].find(x => x > 1);
const promise = Promise.resolve(42);
const obj = Object.assign({}, source);
```

**3. Progressive Web Apps:**

```javascript
// Service Worker polyfill for older browsers
if ('serviceWorker' in navigator) {
  navigator.serviceWorker.register('/sw.js');
} else {
  // Load serviceworker-polyfill for very old browsers
  import('serviceworker-polyfill').then(() => {
    navigator.serviceWorker.register('/sw.js');
  });
}
```

**Loading Polyfills Strategically:**

**1. Conditional Loading:**

```javascript
// Only load polyfills if needed
const polyfillsNeeded = [];

if (!window.Promise) {
  polyfillsNeeded.push(import('promise-polyfill'));
}

if (!window.fetch) {
  polyfillsNeeded.push(import('whatwg-fetch'));
}

if (!Array.prototype.includes) {
  polyfillsNeeded.push(import('core-js/features/array/includes'));
}

// Load all needed polyfills
Promise.all(polyfillsNeeded).then(() => {
  // Initialize app after polyfills loaded
  initApp();
});
```

**2. Using Polyfill Service:**

```html
<!-- Polyfill.io automatically serves only needed polyfills -->
<script src="https://polyfill.io/v3/polyfill.min.js"></script>

<!-- Specify features -->
<script src="https://polyfill.io/v3/polyfill.min.js?features=Promise,fetch,Array.prototype.includes"></script>

<!-- Or let it detect automatically -->
<script crossorigin="anonymous" src="https://polyfill.io/v3/polyfill.min.js"></script>
```

**3. With Babel:**

```javascript
// babel.config.js - Automatic polyfill injection
module.exports = {
  presets: [
    ['@babel/preset-env', {
      useBuiltIns: 'usage', // Only include polyfills you use
      corejs: 3,
      targets: '> 0.25%, not dead'
    }]
  ]
};

// Babel automatically adds imports
// Input
const arr = [1, 2, 3];
arr.includes(2);

// Output (Babel adds polyfill import automatically)
import "core-js/modules/es.array.includes.js";
const arr = [1, 2, 3];
arr.includes(2);
```

**Popular Polyfill Libraries:**

**1. Core-js:**

```javascript
// Import all polyfills
import 'core-js/stable';

// Import specific polyfills
import 'core-js/features/promise';
import 'core-js/features/array/includes';
import 'core-js/features/string/starts-with';

// Use proposals (experimental features)
import 'core-js/proposals/promise-any';
```

**2. Regenerator Runtime:**

```javascript
// For async/await and generators
import 'regenerator-runtime/runtime';

// Now you can use async/await in older browsers
async function fetchData() {
  const response = await fetch('/api/data');
  return response.json();
}
```

**3. Individual Polyfills:**

```bash
# Install specific polyfills
npm install promise-polyfill
npm install whatwg-fetch
npm install intersection-observer
npm install web-animations-js
npm install smoothscroll-polyfill
```

**Real-World Example:**

```javascript
// polyfills.js - Centralized polyfill management
export async function loadPolyfills() {
  const polyfills = [];
  
  // Check and load Promise
  if (!window.Promise) {
    polyfills.push(
      import('promise-polyfill/src/polyfill')
    );
  }
  
  // Check and load Fetch
  if (!window.fetch) {
    polyfills.push(
      import('whatwg-fetch')
    );
  }
  

  // Check and load IntersectionObserver
  if (!('IntersectionObserver' in window)) {
    polyfills.push(
      import('intersection-observer')
    );
  }
  
  // Check and load Object.assign
  if (!Object.assign) {
    polyfills.push(
      import('core-js/features/object/assign')
    );
  }
  
  // Check and load Array methods
  if (!Array.prototype.find) {
    polyfills.push(
      import('core-js/features/array/find')
    );
  }
  
  if (!Array.prototype.includes) {
    polyfills.push(
      import('core-js/features/array/includes')
    );
  }
  
  // Check and load String methods
  if (!String.prototype.startsWith) {
    polyfills.push(
      import('core-js/features/string/starts-with')
    );
  }
  
  // Check and load CustomEvent
  if (typeof window.CustomEvent !== 'function') {
    polyfills.push(
      import('custom-event-polyfill')
    );
  }
  
  // Check and load classList for SVG elements
  if (!('classList' in SVGElement.prototype)) {
    polyfills.push(
      import('classlist-polyfill')
    );
  }
  
  // Wait for all polyfills to load
  await Promise.all(polyfills);
  
  console.log(`Loaded ${polyfills.length} polyfills`);
}

// main.js - Use polyfills before initializing app
import { loadPolyfills } from './polyfills.js';

async function init() {
  // Load polyfills first
  await loadPolyfills();
  
  // Now safe to use modern features
  const data = await fetch('/api/data').then(r => r.json());
  const filtered = data.items.find(item => item.active);
  
  // Initialize application
  startApp(filtered);
}

init();
```

**Advanced Polyfill Patterns:**

**1. Feature Detection Helper:**

```javascript
// features.js - Centralized feature detection
export const features = {
  promise: typeof Promise !== 'undefined',
  fetch: typeof fetch !== 'undefined',
  intersectionObserver: 'IntersectionObserver' in window,
  serviceWorker: 'serviceWorker' in navigator,
  webGL: (() => {
    try {
      const canvas = document.createElement('canvas');
      return !!(canvas.getContext('webgl') || canvas.getContext('experimental-webgl'));
    } catch (e) {
      return false;
    }
  })(),
  localStorage: (() => {
    try {
      const test = '__test__';
      localStorage.setItem(test, test);
      localStorage.removeItem(test);
      return true;
    } catch (e) {
      return false;
    }
  })(),
  customElements: 'customElements' in window,
  shadowDOM: 'attachShadow' in Element.prototype,
  webComponents: 'customElements' in window && 'attachShadow' in Element.prototype
};

// Usage
import { features } from './features.js';

if (!features.fetch) {
  await import('whatwg-fetch');
}

if (!features.intersectionObserver) {
  await import('intersection-observer');
}
```

**2. Lazy Loading Polyfills:**

```javascript
// Load polyfills only when specific features are used
class PolyfillLoader {
  constructor() {
    this.loaded = new Set();
  }
  
  async loadIfNeeded(feature, polyfillLoader) {
    if (this.loaded.has(feature)) {
      return;
    }
    
    const isSupported = this.checkFeature(feature);
    
    if (!isSupported) {
      await polyfillLoader();
      this.loaded.add(feature);
      console.log(`Loaded polyfill for: ${feature}`);
    }
  }
  
  checkFeature(feature) {
    const checks = {
      'fetch': () => 'fetch' in window,
      'promise': () => 'Promise' in window,
      'intersectionObserver': () => 'IntersectionObserver' in window,
      'resizeObserver': () => 'ResizeObserver' in window,
      'mutationObserver': () => 'MutationObserver' in window,
      'webAnimations': () => 'animate' in Element.prototype
    };
    
    return checks[feature] ? checks[feature]() : true;
  }
}

const loader = new PolyfillLoader();

// Usage - load only when needed
async function setupIntersectionObserver() {
  await loader.loadIfNeeded('intersectionObserver', () => 
    import('intersection-observer')
  );
  
  // Now safe to use
  const observer = new IntersectionObserver(callback);
  observer.observe(element);
}
```

**3. Differential Serving:**

```javascript
// Serve different bundles based on browser capabilities
// modern-bundle.js - ES6+, no polyfills
// legacy-bundle.js - ES5 + polyfills

// index.html
<script type="module" src="/modern-bundle.js"></script>
<script nomodule src="/legacy-bundle.js"></script>

// Modern browsers load module script
// Older browsers load nomodule script with polyfills
```

**4. Smart Polyfill Loading:**

```javascript
// Check user's browser and load appropriate polyfills
function getRequiredPolyfills() {
  const userAgent = navigator.userAgent;
  const polyfills = [];
  
  // IE 11
  if (userAgent.indexOf('Trident/') > -1) {
    polyfills.push('promise', 'fetch', 'array-methods', 'object-methods');
  }
  
  // Old Edge (pre-Chromium)
  if (userAgent.indexOf('Edge/') > -1) {
    polyfills.push('fetch');
  }
  
  // Old Safari
  const safariMatch = userAgent.match(/Version\/(\d+).*Safari/);
  if (safariMatch && parseInt(safariMatch[1]) < 12) {
    polyfills.push('promise', 'fetch');
  }
  
  return polyfills;
}

async function loadRequiredPolyfills() {
  const required = getRequiredPolyfills();
  const loaders = {
    'promise': () => import('promise-polyfill'),
    'fetch': () => import('whatwg-fetch'),
    'array-methods': () => import('core-js/features/array'),
    'object-methods': () => import('core-js/features/object')
  };
  
  await Promise.all(
    required.map(name => loaders[name]())
  );
}
```

**Common Polyfill Scenarios:**

**1. Form Validation:**

```javascript
// HTML5 form validation for older browsers
if (!('validity' in document.createElement('input'))) {
  // Load form validation polyfill
  import('form-validity-polyfill').then(() => {
    // Now can use constraint validation API
    const input = document.querySelector('input[type="email"]');
    if (!input.validity.valid) {
      console.log(input.validationMessage);
    }
  });
}
```

**2. Date/Time APIs:**

```javascript
// Intl polyfill for date formatting
if (!window.Intl) {
  await import('intl');
  await import('intl/locale-data/jsonp/en.js');
}

// Now safe to use
const formatter = new Intl.DateTimeFormat('en-US', {
  year: 'numeric',
  month: 'long',
  day: 'numeric'
});

console.log(formatter.format(new Date()));
```

**3. Web Components:**

```javascript
// Polyfill for Web Components
async function loadWebComponentsPolyfills() {
  if (!window.customElements) {
    await import('@webcomponents/webcomponentsjs/webcomponents-loader.js');
  }
  
  // Now can define custom elements
  class MyElement extends HTMLElement {
    connectedCallback() {
      this.innerHTML = '<p>Custom Element</p>';
    }
  }
  
  customElements.define('my-element', MyElement);
}
```

**4. Smooth Scrolling:**

```javascript
// Smooth scroll behavior polyfill
if (!('scrollBehavior' in document.documentElement.style)) {
  import('smoothscroll-polyfill').then(smoothscroll => {
    smoothscroll.polyfill();
    
    // Now smooth scrolling works
    window.scrollTo({
      top: 1000,
      behavior: 'smooth'
    });
  });
}
```

**Best Practices:**

**1. Load Only What You Need:**

```javascript
// ❌ Bad - loading everything
import 'core-js';

// ✅ Good - loading specific features
import 'core-js/features/promise';
import 'core-js/features/array/includes';
```

**2. Use Feature Detection:**

```javascript
// ❌ Bad - no detection
import 'promise-polyfill';

// ✅ Good - conditional loading
if (!window.Promise) {
  import('promise-polyfill');
}
```

**3. Consider Bundle Size:**

```javascript
// Check polyfill sizes before including
// Use bundle analyzers to see impact

// webpack-bundle-analyzer
npm install --save-dev webpack-bundle-analyzer

// Add to webpack config
const BundleAnalyzerPlugin = require('webpack-bundle-analyzer').BundleAnalyzerPlugin;

module.exports = {
  plugins: [
    new BundleAnalyzerPlugin()
  ]
};
```

**4. Test Without Polyfills:**

```javascript
// Temporarily disable polyfills to test native support
// This helps identify unnecessary polyfills

if (process.env.NODE_ENV !== 'test-native') {
  loadPolyfills();
}
```

**5. Document Polyfill Requirements:**

```javascript
// polyfills.md
/**
 * Required Polyfills:
 * 
 * - Promise (IE11)
 * - fetch (IE11, old Edge)
 * - Array.includes (IE11)
 * - Object.assign (IE11)
 * - IntersectionObserver (IE11, old Safari)
 * 
 * Optional Polyfills:
 * 
 * - ResizeObserver (older browsers)
 * - Web Animations (IE11, old Safari)
 * - CustomEvent (IE9-11)
 * 
 * Browser Support Target:
 * > 0.5%, last 2 versions, not dead, IE 11
 */
```

**Performance Considerations:**

```javascript
// Measure polyfill loading impact
console.time('polyfills');
await loadPolyfills();
console.timeEnd('polyfills');

// Monitor bundle size
// Before polyfills: 50KB
// After polyfills: 120KB (+70KB)

// Consider CDN for polyfills
<script src="https://cdn.jsdelivr.net/npm/core-js-bundle@3.25.0/minified.js"></script>

// Or use differential serving
// - Modern bundle: 50KB (no polyfills)
// - Legacy bundle: 120KB (with polyfills)
// Modern browsers get smaller bundle
```

**Alternatives to Polyfills:**

```javascript
// 1. Progressive Enhancement
// Provide basic functionality without the feature
if ('IntersectionObserver' in window) {
  // Use lazy loading
  setupLazyLoading();
} else {
  // Load all images immediately
  loadAllImages();
}

// 2. Graceful Degradation
// Detect and inform users
if (!window.Promise) {
  showBrowserUpgradeMessage();
} else {
  initializeApp();
}

// 3. Feature-Based Loading
// Only load features browser supports
const features = detectFeatures();
loadComponents(features);
```

**When NOT to Use Polyfills:**

1. **Feature is purely aesthetic** - Don't polyfill for minor visual enhancements
2. **Polyfill is too large** - If polyfill adds 200KB, consider alternatives
3. **Feature has good fallback** - Use progressive enhancement instead
4. **Very few users affected** - If < 0.1% users, may not be worth it
5. **Security concerns** - Some polyfills may have vulnerabilities
6. **Performance impact** - If polyfill significantly slows down app

**Summary:**

Polyfills are essential for:
- Supporting older browsers while using modern features
- Ensuring consistent behavior across browsers
- Enabling progressive enhancement strategies
- Maintaining backward compatibility

Use them wisely by:
- Loading conditionally based on feature detection
- Choosing lightweight, well-maintained libraries
- Monitoring bundle size impact
- Testing both with and without polyfills
- Documenting requirements and browser support targets


# JavaScript and the DOM (84-88)

## 84. What is the Document Object Model (DOM)?

The Document Object Model (DOM) is a programming interface for HTML and XML documents. It represents the page structure as a tree of objects that can be manipulated with JavaScript, allowing you to dynamically change the document's structure, style, and content.

**Key Concepts:**

**1. Tree Structure:**

The DOM represents documents as a hierarchical tree of nodes:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>My Page</title>
  </head>
  <body>
    <h1>Welcome</h1>
    <p>Hello World</p>
  </body>
</html>
```

```
Document
  └─ html (Element Node)
      ├─ head (Element Node)
      │   └─ title (Element Node)
      │       └─ "My Page" (Text Node)
      └─ body (Element Node)
          ├─ h1 (Element Node)
          │   └─ "Welcome" (Text Node)
          └─ p (Element Node)
              └─ "Hello World" (Text Node)
```

**2. Node Types:**

The DOM consists of different types of nodes:

```javascript
// Element Node (type 1) - HTML elements
const div = document.createElement('div');
console.log(div.nodeType); // 1
console.log(div.nodeName); // "DIV"

// Text Node (type 3) - Text content
const text = document.createTextNode('Hello');
console.log(text.nodeType); // 3
console.log(text.nodeName); // "#text"

// Comment Node (type 8) - HTML comments
const comment = document.createComment('This is a comment');
console.log(comment.nodeType); // 8
console.log(comment.nodeName); // "#comment"

// Document Node (type 9) - The document itself
console.log(document.nodeType); // 9
console.log(document.nodeName); // "#document"

// Attribute Node (deprecated but still exists)
// Now accessed via Element.attributes
```

**3. DOM Properties and Methods:**

```javascript
// Accessing the document
console.log(document.documentElement); // <html> element
console.log(document.head); // <head> element
console.log(document.body); // <body> element
console.log(document.title); // Page title

// Document information
console.log(document.URL); // Full URL
console.log(document.domain); // Domain name
console.log(document.referrer); // Referring URL
console.log(document.lastModified); // Last modification date

// Document state
console.log(document.readyState); // 'loading', 'interactive', or 'complete'
```

**4. Element Properties:**

```javascript
const element = document.querySelector('.my-element');

// Content properties
console.log(element.innerHTML); // HTML content including tags
console.log(element.textContent); // Text content only
console.log(element.innerText); // Visible text only

// Structure properties
console.log(element.tagName); // Tag name in uppercase
console.log(element.id); // Element ID
console.log(element.className); // CSS classes (string)
console.log(element.classList); // CSS classes (DOMTokenList)

// Hierarchy properties
console.log(element.parentNode); // Parent node
console.log(element.parentElement); // Parent element
console.log(element.childNodes); // All child nodes (NodeList)
console.log(element.children); // Child elements only (HTMLCollection)
console.log(element.firstChild); // First child node
console.log(element.firstElementChild); // First child element
console.log(element.lastChild); // Last child node
console.log(element.lastElementChild); // Last child element
console.log(element.nextSibling); // Next sibling node
console.log(element.nextElementSibling); // Next sibling element
console.log(element.previousSibling); // Previous sibling node
console.log(element.previousElementSibling); // Previous sibling element
```

**5. Attributes:**

```javascript
const element = document.querySelector('img');

// Get attributes
console.log(element.getAttribute('src'));
console.log(element.getAttribute('alt'));

// Set attributes
element.setAttribute('src', 'new-image.jpg');
element.setAttribute('alt', 'New description');

// Remove attributes
element.removeAttribute('title');

// Check if attribute exists
console.log(element.hasAttribute('src')); // true

// Get all attributes
const attrs = element.attributes;
for (let attr of attrs) {
  console.log(`${attr.name}: ${attr.value}`);
}

// Direct property access (for standard attributes)
element.src = 'image.jpg';
element.alt = 'Description';
element.id = 'myImage';
element.className = 'img-responsive';

// Data attributes
element.setAttribute('data-user-id', '123');
console.log(element.dataset.userId); // '123' (camelCase conversion)
element.dataset.userName = 'John';
console.log(element.getAttribute('data-user-name')); // 'John'
```

**6. Styles:**

```javascript
const element = document.querySelector('.box');

// Inline styles (CSS properties in camelCase)
element.style.backgroundColor = 'red';
element.style.fontSize = '20px';
element.style.marginTop = '10px';

// Multiple styles
element.style.cssText = 'background-color: blue; color: white; padding: 10px;';

// Get computed styles (including CSS from stylesheets)
const styles = window.getComputedStyle(element);
console.log(styles.backgroundColor); // Computed background color
console.log(styles.width); // Computed width
console.log(styles.getPropertyValue('font-size')); // Alternative syntax
```

**7. Classes:**

```javascript
const element = document.querySelector('.menu');

// classList API (modern, preferred)
element.classList.add('active');
element.classList.add('visible', 'highlighted'); // Multiple classes
element.classList.remove('hidden');
element.classList.toggle('open'); // Add if absent, remove if present
element.classList.toggle('special', true); // Force add
element.classList.replace('old-class', 'new-class');
console.log(element.classList.contains('active')); // true

// className (string manipulation, older approach)
element.className = 'menu active'; // Replace all classes
element.className += ' highlighted'; // Add class (note the space)
```

**8. DOM Events:**

```javascript
const button = document.querySelector('button');

// Add event listener
button.addEventListener('click', function(event) {
  console.log('Button clicked!');
  console.log('Event type:', event.type);
  console.log('Target element:', event.target);
  console.log('Current target:', event.currentTarget);
});

// Event with options
button.addEventListener('click', handler, {
  once: true,      // Remove after first trigger
  capture: false,  // Use bubbling phase
  passive: true    // Won't call preventDefault()
});

// Remove event listener
function handler() {
  console.log('Clicked');
}
button.addEventListener('click', handler);
button.removeEventListener('click', handler);

// Event delegation
document.querySelector('.list').addEventListener('click', function(event) {
  if (event.target.matches('li')) {
    console.log('List item clicked:', event.target.textContent);
  }
});
```

**9. DOM Traversal:**

```javascript
const element = document.querySelector('.current');

// Moving up
console.log(element.parentNode);
console.log(element.parentElement);
console.log(element.closest('.container')); // Nearest ancestor matching selector

// Moving down
console.log(element.children); // Direct children (elements only)
console.log(element.childNodes); // All child nodes
console.log(element.querySelector('.child')); // First matching descendant
console.log(element.querySelectorAll('.child')); // All matching descendants

// Moving sideways
console.log(element.nextElementSibling);
console.log(element.previousElementSibling);

// Complex traversal
function getAllSiblings(element) {
  const siblings = [];
  let sibling = element.parentElement.firstElementChild;
  
  while (sibling) {
    if (sibling !== element) {
      siblings.push(sibling);
    }
    sibling = sibling.nextElementSibling;
  }
  
  return siblings;
}
```

**10. DOM Dimensions and Position:**

```javascript
const element = document.querySelector('.box');

// Size (including padding, excluding margin and border)
console.log(element.clientWidth);
console.log(element.clientHeight);

// Size (including padding and border)
console.log(element.offsetWidth);
console.log(element.offsetHeight);

// Size (including padding, border, and scrollbar)
console.log(element.scrollWidth);
console.log(element.scrollHeight);

// Position relative to offset parent
console.log(element.offsetLeft);
console.log(element.offsetTop);
console.log(element.offsetParent);

// Scroll position
console.log(element.scrollLeft);
console.log(element.scrollTop);

// Bounding rectangle (position relative to viewport)
const rect = element.getBoundingClientRect();
console.log(rect.top, rect.right, rect.bottom, rect.left);
console.log(rect.width, rect.height);
console.log(rect.x, rect.y); // Same as left and top
```

**Real-World Example:**

```javascript
// Building a simple todo list with DOM manipulation
class TodoList {
  constructor(containerId) {
    this.container = document.getElementById(containerId);
    this.todos = [];
    this.render();
  }
  
  addTodo(text) {
    const todo = {
      id: Date.now(),
      text: text,
      completed: false
    };
    
    this.todos.push(todo);
    this.render();
  }
  
  toggleTodo(id) {
    const todo = this.todos.find(t => t.id === id);
    if (todo) {
      todo.completed = !todo.completed;
      this.render();
    }
  }
  
  deleteTodo(id) {
    this.todos = this.todos.filter(t => t.id !== id);
    this.render();
  }
  
  render() {
    // Clear container
    this.container.innerHTML = '';
    
    // Create list
    const ul = document.createElement('ul');
    ul.className = 'todo-list';
    
    // Add todos
    this.todos.forEach(todo => {
      const li = document.createElement('li');
      li.className = todo.completed ? 'completed' : '';
      li.setAttribute('data-id', todo.id);
      
      const checkbox = document.createElement('input');
      checkbox.type = 'checkbox';
      checkbox.checked = todo.completed;
      checkbox.addEventListener('change', () => this.toggleTodo(todo.id));
      
      const text = document.createElement('span');
      text.textContent = todo.text;
      
      const deleteBtn = document.createElement('button');
      deleteBtn.textContent = 'Delete';
      deleteBtn.addEventListener('click', () => this.deleteTodo(todo.id));
      
      li.appendChild(checkbox);
      li.appendChild(text);
      li.appendChild(deleteBtn);
      ul.appendChild(li);
    });
    
    this.container.appendChild(ul);
  }
}

// Usage
const todoList = new TodoList('todo-container');
todoList.addTodo('Learn JavaScript');
todoList.addTodo('Master the DOM');
```

**DOM vs Virtual DOM:**

```javascript
// Traditional DOM manipulation (can be slow with many updates)
for (let i = 0; i < 1000; i++) {
  const div = document.createElement('div');
  div.textContent = `Item ${i}`;
  document.body.appendChild(div); // Each append triggers reflow
}

// Better approach - batch updates
const fragment = document.createDocumentFragment();
for (let i = 0; i < 1000; i++) {
  const div = document.createElement('div');
  div.textContent = `Item ${i}`;
  fragment.appendChild(div);
}
document.body.appendChild(fragment); // Single reflow

// Virtual DOM (React example) - framework handles optimization
function TodoList({ todos }) {
  return (
    <ul>
      {todos.map(todo => (
        <li key={todo.id}>{todo.text}</li>
      ))}
    </ul>
  );
}
```

**Browser Rendering Process:**

```javascript
// Understanding how DOM changes affect rendering

// 1. DOM Tree - Structure of the page
// 2. CSSOM Tree - Styles applied
// 3. Render Tree - Combines DOM + CSSOM
// 4. Layout (Reflow) - Calculate positions and sizes
// 5. Paint - Draw pixels on screen
// 6. Composite - Combine layers

// Operations that trigger reflow (expensive):
element.offsetWidth; // Reading layout properties
element.style.width = '100px'; // Changing layout properties
element.classList.add('new-class'); // If affects layout

// Operations that only trigger repaint (less expensive):
element.style.color = 'red';
element.style.backgroundColor = 'blue';

// Optimizing DOM operations
// ❌ Bad - multiple reflows
element.style.width = '100px';
element.style.height = '100px';
element.style.margin = '10px';

// ✅ Good - single reflow
element.style.cssText = 'width: 100px; height: 100px; margin: 10px;';

// Or use classes
element.classList.add('resized');
```

**Key Takeaways:**

1. **DOM is an API** - Interface to interact with HTML documents
2. **Tree structure** - Hierarchical organization of nodes
3. **Live collection** - DOM updates reflect immediately in the page
4. **Cross-browser** - Standardized API works in all modern browsers
5. **Performance matters** - Minimize reflows and repaints
6. **Event-driven** - Interact with user actions through events



## 85. How do you create, append, or remove an element from the DOM?

DOM manipulation allows you to dynamically create, modify, and remove elements. Here are comprehensive methods for each operation:

**Creating Elements:**

**1. createElement() - Most Common Method:**

```javascript
// Create an element
const div = document.createElement('div');
const paragraph = document.createElement('p');
const button = document.createElement('button');
const image = document.createElement('img');

// Set properties
div.id = 'myDiv';
div.className = 'container';
paragraph.textContent = 'Hello World';
button.textContent = 'Click Me';
image.src = 'photo.jpg';
image.alt = 'Description';

// Set attributes
div.setAttribute('data-role', 'main');
button.setAttribute('type', 'button');

// Add styles
div.style.backgroundColor = 'lightblue';
div.style.padding = '20px';
```

**2. createTextNode() - Create Text Nodes:**

```javascript
// Create text node
const textNode = document.createTextNode('This is plain text');

// Create element and add text
const paragraph = document.createElement('p');
paragraph.appendChild(textNode);
```

**3. createDocumentFragment() - Efficient Batch Creation:**

```javascript
// Create fragment (not part of DOM tree initially)
const fragment = document.createDocumentFragment();

// Add multiple elements to fragment
for (let i = 0; i < 100; i++) {
  const li = document.createElement('li');
  li.textContent = `Item ${i}`;
  fragment.appendChild(li);
}

// Single DOM insertion (better performance)
document.querySelector('ul').appendChild(fragment);
```

**4. cloneNode() - Clone Existing Elements:**

```javascript
const original = document.querySelector('.template');

// Shallow clone (element only, no children)
const shallowClone = original.cloneNode(false);

// Deep clone (element with all descendants)
const deepClone = original.cloneNode(true);

// Modify and append clone
deepClone.id = 'clone-1';
deepClone.textContent = 'Cloned content';
document.body.appendChild(deepClone);
```

**5. innerHTML (String-based Creation):**

```javascript
// Create elements from HTML string
const container = document.createElement('div');
container.innerHTML = `
  <h2>Title</h2>
  <p>Paragraph text</p>
  <button class="btn">Click</button>
`;

// ⚠️ Warning: innerHTML can be unsafe with user input
// Always sanitize user data
const userInput = getUserInput();
const sanitized = DOMPurify.sanitize(userInput); // Use a library
container.innerHTML = sanitized;
```

**Appending Elements:**

**1. appendChild() - Add as Last Child:**

```javascript
const parent = document.querySelector('.parent');
const child = document.createElement('div');
child.textContent = 'New child';

// Add as last child
parent.appendChild(child);

// Move existing element (removes from old position)
const existingElement = document.querySelector('.move-me');
parent.appendChild(existingElement);
```

**2. append() - Modern Method (Multiple Nodes):**

```javascript
const parent = document.querySelector('.parent');

// Append multiple nodes at once
parent.append(
  document.createElement('div'),
  'Text node',
  document.createElement('span')
);

// Can mix elements and strings
parent.append('Hello ', document.createElement('strong'), ' World');
```

**3. prepend() - Add as First Child:**

```javascript
const parent = document.querySelector('.parent');
const child = document.createElement('div');

// Add as first child
parent.prepend(child);

// Multiple elements
parent.prepend(
  document.createElement('header'),
  document.createElement('nav')
);
```

**4. insertBefore() - Insert Before Specific Element:**

```javascript
const parent = document.querySelector('.parent');
const newElement = document.createElement('div');
const referenceElement = document.querySelector('.reference');

// Insert newElement before referenceElement
parent.insertBefore(newElement, referenceElement);

// Insert as first child (before first child)
parent.insertBefore(newElement, parent.firstChild);
```

**5. insertAdjacentElement() - Flexible Positioning:**

```javascript
const reference = document.querySelector('.reference');
const newElement = document.createElement('div');

// Four positions:
// 'beforebegin' - Before the element itself
reference.insertAdjacentElement('beforebegin', newElement);

// 'afterbegin' - First child of the element
reference.insertAdjacentElement('afterbegin', newElement);

// 'beforeend' - Last child of the element
reference.insertAdjacentElement('beforeend', newElement);

// 'afterend' - After the element itself
reference.insertAdjacentElement('afterend', newElement);
```

**6. insertAdjacentHTML() - Insert HTML String:**

```javascript
const element = document.querySelector('.target');

// Insert HTML at different positions
element.insertAdjacentHTML('beforebegin', '<div>Before</div>');
element.insertAdjacentHTML('afterbegin', '<p>Start of content</p>');
element.insertAdjacentHTML('beforeend', '<p>End of content</p>');
element.insertAdjacentHTML('afterend', '<div>After</div>');
```

**7. after() and before() - Modern Methods:**

```javascript
const element = document.querySelector('.target');

// Insert after element
element.after(
  document.createElement('div'),
  'Text content'
);

// Insert before element
element.before(
  document.createElement('header'),
  document.createElement('nav')
);
```

**Removing Elements:**

**1. remove() - Modern Method (Simplest):**

```javascript
const element = document.querySelector('.to-remove');

// Remove element from DOM
element.remove();

// Remove multiple elements
document.querySelectorAll('.temp').forEach(el => el.remove());
```

**2. removeChild() - Traditional Method:**

```javascript
const parent = document.querySelector('.parent');
const child = document.querySelector('.child');

// Remove specific child
parent.removeChild(child);

// Remove first child
if (parent.firstChild) {
  parent.removeChild(parent.firstChild);
}

// Remove last child
if (parent.lastChild) {
  parent.removeChild(parent.lastChild);
}
```

**3. Remove All Children:**

```javascript
const parent = document.querySelector('.parent');

// Method 1: innerHTML (fastest but loses event listeners)
parent.innerHTML = '';

// Method 2: textContent (also fast, same caveat)
parent.textContent = '';

// Method 3: replaceChildren() - modern, clean
parent.replaceChildren();

// Method 4: Loop with removeChild (preserves cleanup)
while (parent.firstChild) {
  parent.removeChild(parent.firstChild);
}

// Method 5: Loop with remove()
parent.childNodes.forEach(child => child.remove());
```

**4. replaceChild() - Replace Element:**

```javascript
const parent = document.querySelector('.parent');
const oldElement = document.querySelector('.old');
const newElement = document.createElement('div');
newElement.textContent = 'New content';

// Replace old with new
parent.replaceChild(newElement, oldElement);
```

**5. replaceWith() - Modern Replacement:**

```javascript
const oldElement = document.querySelector('.old');
const newElement = document.createElement('div');

// Replace element
oldElement.replaceWith(newElement);

// Replace with multiple nodes
oldElement.replaceWith(
  document.createElement('header'),
  'Text',
  document.createElement('footer')
);
```

**Real-World Examples:**

**1. Building a Dynamic List:**

```javascript
function createTodoList(items) {
  // Create container
  const ul = document.createElement('ul');
  ul.className = 'todo-list';
  
  // Create fragment for performance
  const fragment = document.createDocumentFragment();
  
  // Add items
  items.forEach(item => {
    const li = document.createElement('li');
    
    // Checkbox
    const checkbox = document.createElement('input');
    checkbox.type = 'checkbox';
    checkbox.checked = item.completed;
    checkbox.addEventListener('change', () => toggleTodo(item.id));
    
    // Text
    const span = document.createElement('span');
    span.textContent = item.text;
    if (item.completed) {
      span.style.textDecoration = 'line-through';
    }
    
    // Delete button
    const deleteBtn = document.createElement('button');
    deleteBtn.textContent = '×';
    deleteBtn.className = 'delete-btn';
    deleteBtn.addEventListener('click', () => deleteTodo(item.id));
    
    // Assemble
    li.appendChild(checkbox);
    li.appendChild(span);
    li.appendChild(deleteBtn);
    fragment.appendChild(li);
  });
  
  ul.appendChild(fragment);
  return ul;
}

// Usage
const todos = [
  { id: 1, text: 'Learn DOM', completed: false },
  { id: 2, text: 'Build project', completed: false }
];

const list = createTodoList(todos);
document.querySelector('.container').appendChild(list);
```

**2. Creating a Card Component:**

```javascript
function createCard(data) {
  // Create card structure
  const card = document.createElement('div');
  card.className = 'card';
  card.setAttribute('data-id', data.id);
  
  // Card image
  const img = document.createElement('img');
  img.src = data.image;
  img.alt = data.title;
  img.className = 'card-img';
  
  // Card body
  const body = document.createElement('div');
  body.className = 'card-body';
  
  // Title
  const title = document.createElement('h3');
  title.className = 'card-title';
  title.textContent = data.title;
  
  // Description
  const description = document.createElement('p');
  description.className = 'card-description';
  description.textContent = data.description;
  
  // Button
  const button = document.createElement('button');
  button.className = 'btn btn-primary';
  button.textContent = 'Learn More';
  button.addEventListener('click', () => showDetails(data.id));
  
  // Assemble card
  body.append(title, description, button);
  card.append(img, body);
  
  return card;
}

// Usage
const cardData = {
  id: 1,
  image: 'product.jpg',
  title: 'Product Name',
  description: 'Product description here'
};

const card = createCard(cardData);
document.querySelector('.products').appendChild(card);
```

**3. Table Generation:**

```javascript
function createTable(data) {
  const table = document.createElement('table');
  table.className = 'data-table';
  
  // Create thead
  const thead = document.createElement('thead');
  const headerRow = document.createElement('tr');
  
  // Get headers from first object
  const headers = Object.keys(data[0]);
  headers.forEach(header => {
    const th = document.createElement('th');
    th.textContent = header.charAt(0).toUpperCase() + header.slice(1);
    headerRow.appendChild(th);
  });
  
  thead.appendChild(headerRow);
  
  // Create tbody
  const tbody = document.createElement('tbody');
  
  data.forEach(row => {
    const tr = document.createElement('tr');
    
    headers.forEach(header => {
      const td = document.createElement('td');
      td.textContent = row[header];
      tr.appendChild(td);
    });
    
    tbody.appendChild(tr);
  });
  
  // Assemble table
  table.appendChild(thead);
  table.appendChild(tbody);
  
  return table;
}

// Usage
const tableData = [
  { name: 'John', age: 30, city: 'New York' },
  { name: 'Jane', age: 25, city: 'London' },
  { name: 'Bob', age: 35, city: 'Paris' }
];

const table = createTable(tableData);
document.querySelector('.table-container').appendChild(table);
```

**4. Modal Creation and Removal:**

```javascript
function showModal(title, content) {
  // Create modal structure
  const modal = document.createElement('div');
  modal.className = 'modal';
  modal.id = 'dynamic-modal';
  
  const modalContent = document.createElement('div');
  modalContent.className = 'modal-content';
  
  // Close button
  const closeBtn = document.createElement('button');
  closeBtn.className = 'modal-close';
  closeBtn.textContent = '×';
  closeBtn.addEventListener('click', () => closeModal());
  
  // Title
  const modalTitle = document.createElement('h2');
  modalTitle.textContent = title;
  
  // Content
  const modalBody = document.createElement('div');
  modalBody.className = 'modal-body';
  modalBody.innerHTML = content; // Or use textContent for safety
  
  // Assemble modal
  modalContent.append(closeBtn, modalTitle, modalBody);
  modal.appendChild(modalContent);
  
  // Add to page
  document.body.appendChild(modal);
  
  // Backdrop click to close
  modal.addEventListener('click', (e) => {
    if (e.target === modal) {
      closeModal();
    }
  });
  
  // Show with animation
  setTimeout(() => modal.classList.add('show'), 10);
}

function closeModal() {
  const modal = document.getElementById('dynamic-modal');
  if (modal) {
    modal.classList.remove('show');
    setTimeout(() => modal.remove(), 300); // Remove after animation
  }
}

// Usage
showModal('Welcome', '<p>This is a dynamic modal!</p>');
```

**5. Drag and Drop List Reordering:**

```javascript
function createDraggableList(items) {
  const ul = document.createElement('ul');
  ul.className = 'draggable-list';
  
  items.forEach((item, index) => {
    const li = document.createElement('li');
    li.textContent = item;
    li.draggable = true;
    li.setAttribute('data-index', index);
    
    // Drag events
    li.addEventListener('dragstart', handleDragStart);
    li.addEventListener('dragover', handleDragOver);
    li.addEventListener('drop', handleDrop);
    li.addEventListener('dragend', handleDragEnd);
    
    ul.appendChild(li);
  });
  
  return ul;
}

let draggedElement = null;

function handleDragStart(e) {
  draggedElement = this;
  this.classList.add('dragging');
  e.dataTransfer.effectAllowed = 'move';
}

function handleDragOver(e) {
  if (e.preventDefault) {
    e.preventDefault();
  }
  e.dataTransfer.dropEffect = 'move';
  return false;
}

function handleDrop(e) {
  if (e.stopPropagation) {
    e.stopPropagation();
  }
  
  if (draggedElement !== this) {
    // Reorder elements
    const parent = this.parentNode;
    const allItems = [...parent.children];
    const draggedIndex = allItems.indexOf(draggedElement);
    const targetIndex = allItems.indexOf(this);
    
    if (draggedIndex < targetIndex) {
      parent.insertBefore(draggedElement, this.nextSibling);
    } else {
      parent.insertBefore(draggedElement, this);
    }
  }
  
  return false;
}

function handleDragEnd(e) {
  this.classList.remove('dragging');
  document.querySelectorAll('.draggable-list li').forEach(li => {
    li.classList.remove('over');
  });
}

// Usage
const items = ['Item 1', 'Item 2', 'Item 3', 'Item 4'];
const list = createDraggableList(items);
document.querySelector('.container').appendChild(list);
```

**Performance Best Practices:**

```javascript
// ❌ Bad - Multiple reflows
for (let i = 0; i < 1000; i++) {
  const div = document.createElement('div');
  div.textContent = `Item ${i}`;
  document.body.appendChild(div); // Reflow on each append
}

// ✅ Good - Single reflow with fragment
const fragment = document.createDocumentFragment();
for (let i = 0; i < 1000; i++) {
  const div = document.createElement('div');
  div.textContent = `Item ${i}`;
  fragment.appendChild(div);
}
document.body.appendChild(fragment); // Single reflow

// ✅ Good - Batch with innerHTML (if no event listeners needed)
const html = Array.from({ length: 1000 }, (_, i) => 
  `<div>Item ${i}</div>`
).join('');
document.body.innerHTML += html;

// ❌ Bad - Reading and writing layout properties
element.style.width = element.offsetWidth + 10 + 'px'; // Forces reflow

// ✅ Good - Batch reads and writes
const width = element.offsetWidth; // Read
element.style.width = width + 10 + 'px'; // Write
```

**Common Pitfalls:**

```javascript
// 1. Event listeners on removed elements
const button = document.createElement('button');
button.addEventListener('click', handleClick);
document.body.appendChild(button);
button.remove(); // Event listener still in memory if handleClick has closure

// Solution: Remove listeners before removing elements
button.removeEventListener('click', handleClick);
button.remove();

// 2. innerHTML with event listeners
const parent = document.querySelector('.parent');
parent.innerHTML = '<button onclick="alert()">Click</button>'; // Works
parent.innerHTML = ''; // Loses all event listeners on children

// 3. Live vs Static collections
const divs = document.getElementsByTagName('div'); // Live
const moreDivs = document.querySelectorAll('div'); // Static

document.body.appendChild(document.createElement('div'));
console.log(divs.length); // Increases (live collection)
console.log(moreDivs.length); // Stays same (static snapshot)

// 4. Modifying arrays while iterating
const items = document.querySelectorAll('.item');
items.forEach(item => {
  if (condition) {
    item.remove(); // Safe with querySelectorAll (static)
  }
});

const liveItems = document.getElementsByClassName('item');
// ❌ Bad - collection changes during iteration
for (let i = 0; i < liveItems.length; i++) {
  liveItems[i].remove(); // Skips elements!
}

// ✅ Good - iterate backwards or convert to array
for (let i = liveItems.length - 1; i >= 0; i--) {
  liveItems[i].remove();
}
// Or
[...liveItems].forEach(item => item.remove());
```

**Memory Management:**

```javascript
// Clean up to prevent memory leaks
class Component {
  constructor() {
    this.element = document.createElement('div');
    this.handleClick = this.handleClick.bind(this);
    this.element.addEventListener('click', this.handleClick);
  }
  
  handleClick() {
    console.log('Clicked');
  }
  
  destroy() {
    // Remove event listeners
    this.element.removeEventListener('click', this.handleClick);
    
    // Remove from DOM
    this.element.remove();
    
    // Clear references
    this.element = null;
    this.handleClick = null;
  }
}

// Usage
const component = new Component();
document.body.appendChild(component.element);

// Later, clean up
component.destroy();
```



## 86. Describe different ways to find or access HTML elements in the DOM.

There are multiple methods to select and access HTML elements in the DOM, each with different use cases and performance characteristics.

**Modern Methods (Recommended):**

**1. querySelector() - First Matching Element:**

```javascript
// Select first element matching CSS selector
const element = document.querySelector('.my-class');
const byId = document.querySelector('#my-id');
const byTag = document.querySelector('div');
const complex = document.querySelector('div.container > p:first-child');

// Works on any element, not just document
const parent = document.querySelector('.parent');
const child = parent.querySelector('.child');

// Returns null if not found
const notFound = document.querySelector('.does-not-exist');
console.log(notFound); // null

// Advanced selectors
const input = document.querySelector('input[type="email"]');
const checked = document.querySelector('input:checked');
const disabled = document.querySelector('button:disabled');
const nthChild = document.querySelector('li:nth-child(3)');
const dataAttr = document.querySelector('[data-role="main"]');
```

**2. querySelectorAll() - All Matching Elements:**

```javascript
// Returns NodeList (static snapshot)
const elements = document.querySelectorAll('.item');
console.log(elements.length);

// Iterate with forEach (NodeList has forEach)
elements.forEach(element => {
  console.log(element.textContent);
});

// Convert to array for array methods
const array = Array.from(elements);
const filtered = array.filter(el => el.classList.contains('active'));

// Or use spread operator
const arr = [...elements];

// Multiple selectors (comma-separated)
const multiple = document.querySelectorAll('.class1, .class2, #id1');

// Complex selectors
const specific = document.querySelectorAll('div.container > p.highlighted');
const notSelector = document.querySelectorAll('li:not(.excluded)');
const attributes = document.querySelectorAll('[data-active="true"]');

// Returns empty NodeList if nothing found
const empty = document.querySelectorAll('.nothing');
console.log(empty.length); // 0
```

**Classic Methods:**

**3. getElementById() - Single Element by ID:**

```javascript
// Fastest method for ID lookup
const element = document.getElementById('my-id');

// No '#' prefix needed
// ❌ Wrong
const wrong = document.getElementById('#my-id');

// ✅ Correct
const correct = document.getElementById('my-id');

// Returns null if not found
const notFound = document.getElementById('nonexistent');

// Only available on document object
// ❌ This won't work
const parent = document.querySelector('.parent');
const child = parent.getElementById('child-id'); // Error!

// Note: IDs should be unique in valid HTML
```

**4. getElementsByClassName() - Live HTMLCollection:**

```javascript
// Returns live HTMLCollection
const elements = document.getElementsByClassName('my-class');

// Multiple classes (space-separated)
const multi = document.getElementsByClassName('class1 class2');

// Live collection - updates automatically
console.log(elements.length); // e.g., 3
document.body.appendChild(createElementWithClass('my-class'));
console.log(elements.length); // 4 (automatically updated)

// Can be called on any element
const parent = document.getElementById('container');
const children = parent.getElementsByClassName('child');

// Iterate (no forEach on HTMLCollection in older browsers)
for (let i = 0; i < elements.length; i++) {
  console.log(elements[i]);
}

// Or convert to array
Array.from(elements).forEach(el => {
  console.log(el);
});

// Access by index
const first = elements[0];
const second = elements[1];
```

**5. getElementsByTagName() - Live HTMLCollection by Tag:**

```javascript
// Get all elements of a specific tag
const divs = document.getElementsByTagName('div');
const paragraphs = document.getElementsByTagName('p');
const images = document.getElementsByTagName('img');

// Get all elements
const allElements = document.getElementsByTagName('*');

// Live collection
console.log(divs.length);
document.body.appendChild(document.createElement('div'));
console.log(divs.length); // Increased by 1

// Scoped to an element
const container = document.getElementById('container');
const containerDivs = container.getElementsByTagName('div');

// Case-insensitive in HTML documents
const upper = document.getElementsByTagName('DIV');
const lower = document.getElementsByTagName('div');
// Both return the same elements
```

**6. getElementsByName() - Elements by Name Attribute:**

```javascript
// Useful for form elements
const radios = document.getElementsByName('gender');
const inputs = document.getElementsByName('username');

// Returns live NodeList
console.log(radios.length);

// Iterate
radios.forEach(radio => {
  if (radio.checked) {
    console.log('Selected:', radio.value);
  }
});

// Common use case: radio buttons
function getSelectedRadio(name) {
  const radios = document.getElementsByName(name);
  for (let radio of radios) {
    if (radio.checked) {
      return radio.value;
    }
  }
  return null;
}

const selected = getSelectedRadio('payment-method');
```

**Relationship-Based Selection:**

**7. Parent, Child, and Sibling Access:**

```javascript
const element = document.querySelector('.current');

// Parent relationships
console.log(element.parentNode); // Immediate parent (any node)
console.log(element.parentElement); // Immediate parent (element only)

// Closest ancestor matching selector
const container = element.closest('.container');
const form = element.closest('form');
const body = element.closest('body');

// Children relationships
console.log(element.children); // HTMLCollection of child elements
console.log(element.childNodes); // NodeList of all child nodes (includes text nodes)
console.log(element.firstChild); // First child node
console.log(element.firstElementChild); // First child element
console.log(element.lastChild); // Last child node
console.log(element.lastElementChild); // Last child element
console.log(element.childElementCount); // Number of child elements

// Sibling relationships
console.log(element.nextSibling); // Next sibling node
console.log(element.nextElementSibling); // Next sibling element
console.log(element.previousSibling); // Previous sibling node
console.log(element.previousElementSibling); // Previous sibling element
```

**8. closest() - Find Nearest Ancestor:**

```javascript
const button = document.querySelector('.delete-btn');

// Find nearest parent with specific selector
const card = button.closest('.card');
const container = button.closest('.container');
const form = button.closest('form');

// Can match the element itself
const self = button.closest('.delete-btn'); // Returns button

// Returns null if no match
const notFound = button.closest('.nonexistent');

// Use case: Event delegation
document.querySelector('.list').addEventListener('click', (e) => {
  const item = e.target.closest('.list-item');
  if (item) {
    console.log('Clicked item:', item.dataset.id);
  }
});
```

**9. matches() - Check if Element Matches Selector:**

```javascript
const element = document.querySelector('.item');

// Check if element matches selector
if (element.matches('.active')) {
  console.log('Element is active');
}

if (element.matches('div.item[data-type="primary"]')) {
  console.log('Matches complex selector');
}

// Common use case: Event delegation
document.addEventListener('click', (e) => {
  if (e.target.matches('.button, .link')) {
    handleClick(e);
  }
});

// Check multiple conditions
if (element.matches('.item') && !element.matches('.disabled')) {
  // Element is an enabled item
}
```

**Special Collections:**

**10. forms - All Forms:**

```javascript
// Access all forms
const forms = document.forms;

// Access by index
const firstForm = document.forms[0];

// Access by name attribute
const loginForm = document.forms['login'];
const contactForm = document.forms.contact; // Dot notation

// Iterate
Array.from(document.forms).forEach(form => {
  console.log(form.name);
});
```

**11. images - All Images:**

```javascript
// All img elements
const images = document.images;

// Iterate and lazy load
Array.from(document.images).forEach(img => {
  if (img.dataset.src) {
    img.src = img.dataset.src;
  }
});
```

**12. links - All Links:**

```javascript
// All <a> elements with href attribute
const links = document.links;

// Add external link indicator
Array.from(document.links).forEach(link => {
  if (link.hostname !== window.location.hostname) {
    link.target = '_blank';
    link.rel = 'noopener noreferrer';
  }
});
```

**13. Form Elements:**

```javascript
const form = document.querySelector('form');

// Access form elements
const elements = form.elements;

// By name
const username = form.elements['username'];
const email = form.elements.email;

// By index
const firstInput = form.elements[0];

// Radio button groups
const gender = form.elements['gender']; // RadioNodeList

// Get form data
function getFormData(form) {
  const data = {};
  const elements = form.elements;
  
  for (let element of elements) {
    if (element.name && !element.disabled) {
      if (element.type === 'checkbox') {
        data[element.name] = element.checked;
      } else if (element.type === 'radio') {
        if (element.checked) {
          data[element.name] = element.value;
        }
      } else {
        data[element.name] = element.value;
      }
    }
  }
  
  return data;
}
```

**Advanced Selection Techniques:**

**14. Combining Methods:**

```javascript
// Find all active items in a specific container
const container = document.getElementById('main-container');
const activeItems = container.querySelectorAll('.item.active');

// Find parent, then children
const parent = document.querySelector('.parent');
const children = parent.children;
const firstChild = parent.firstElementChild;

// Complex traversal
const button = document.querySelector('.submit-btn');
const form = button.closest('form');
const inputs = form.querySelectorAll('input[required]');

// Find siblings
const current = document.querySelector('.current');
const next = current.nextElementSibling;
const prev = current.previousElementSibling;
```

**15. Custom Selectors and Utilities:**

```javascript
// Helper function to select with default
function $(selector, context = document) {
  return context.querySelector(selector);
}

function $$(selector, context = document) {
  return Array.from(context.querySelectorAll(selector));
}

// Usage
const element = $('.my-class');
const elements = $$('.item');

// Find by attribute value
function findByAttribute(attr, value) {
  return document.querySelector(`[${attr}="${value}"]`);
}

const element = findByAttribute('data-id', '123');

// Find by text content
function findByText(text, tag = '*') {
  return Array.from(document.querySelectorAll(tag))
    .find(el => el.textContent.trim() === text);
}

const header = findByText('Welcome', 'h1');

// Find by partial text
function findByPartialText(text, tag = '*') {
  return Array.from(document.querySelectorAll(tag))
    .filter(el => el.textContent.includes(text));
}

// Find by data attribute
function findByData(key, value) {
  return document.querySelectorAll(`[data-${key}="${value}"]`);
}

const items = findByData('category', 'electronics');
```

**16. Performance Optimizations:**

```javascript
// Cache selectors (don't query repeatedly)
// ❌ Bad
for (let i = 0; i < 100; i++) {
  document.querySelector('.container').appendChild(element);
}

// ✅ Good
const container = document.querySelector('.container');
for (let i = 0; i < 100; i++) {
  container.appendChild(element);
}

// Use ID for single elements (fastest)
const byId = document.getElementById('unique-id'); // Fast
const byQuery = document.querySelector('#unique-id'); // Slower

// Scope queries to narrow context
// ❌ Bad - searches entire document
const items = document.querySelectorAll('.item');

// ✅ Good - searches within container only
const container = document.getElementById('container');
const items = container.querySelectorAll('.item');

// Use specific selectors
// ❌ Slow - overly broad
const all = document.querySelectorAll('*');

// ✅ Fast - specific
const divs = document.getElementsByTagName('div');
const items = document.getElementsByClassName('item');
```

**17. Handling Dynamic Content:**

```javascript
// Elements added after page load
function waitForElement(selector, timeout = 5000) {
  return new Promise((resolve, reject) => {
    const element = document.querySelector(selector);
    
    if (element) {
      return resolve(element);
    }
    
    const observer = new MutationObserver((mutations) => {
      const element = document.querySelector(selector);
      if (element) {
        observer.disconnect();
        resolve(element);
      }
    });
    
    observer.observe(document.body, {
      childList: true,
      subtree: true
    });
    
    setTimeout(() => {
      observer.disconnect();
      reject(new Error(`Element ${selector} not found within ${timeout}ms`));
    }, timeout);
  });
}

// Usage
waitForElement('.dynamic-content')
  .then(element => {
    console.log('Found element:', element);
  })
  .catch(error => {
    console.error(error);
  });
```

**18. Finding Elements by Position:**

```javascript
// Element at specific coordinates
const element = document.elementFromPoint(x, y);

// All elements at coordinates (stacked)
const elements = document.elementsFromPoint(x, y);

// Use case: Detecting what's under cursor
document.addEventListener('mousemove', (e) => {
  const element = document.elementFromPoint(e.clientX, e.clientY);
  console.log('Hovering over:', element.tagName);
});

// Find elements in viewport
function getElementsInViewport() {
  const elements = document.querySelectorAll('*');
  return Array.from(elements).filter(el => {
    const rect = el.getBoundingClientRect();
    return (
      rect.top >= 0 &&
      rect.left >= 0 &&
      rect.bottom <= window.innerHeight &&
      rect.right <= window.innerWidth
    );
  });
}
```

**Real-World Examples:**

**1. Form Validation:**

```javascript
function validateForm(formId) {
  const form = document.getElementById(formId);
  const requiredFields = form.querySelectorAll('[required]');
  const errors = [];
  
  requiredFields.forEach(field => {
    if (!field.value.trim()) {
      errors.push(`${field.name} is required`);
      field.classList.add('error');
    } else {
      field.classList.remove('error');
    }
  });
  
  // Validate email
  const emailInput = form.querySelector('input[type="email"]');
  if (emailInput && emailInput.value) {
    const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    if (!emailPattern.test(emailInput.value)) {
      errors.push('Invalid email format');
      emailInput.classList.add('error');
    }
  }
  
  return errors;
}
```

**2. Navigation Menu Highlighting:**

```javascript
function highlightCurrentPage() {
  const currentUrl = window.location.pathname;
  const menuLinks = document.querySelectorAll('.nav-menu a');
  
  menuLinks.forEach(link => {
    link.classList.remove('active');
    
    if (link.getAttribute('href') === currentUrl) {
      link.classList.add('active');
      
      // Also highlight parent menu items
      const parentMenu = link.closest('.nav-submenu');
      if (parentMenu) {
        const parentLink = parentMenu.previousElementSibling;
        if (parentLink) {
          parentLink.classList.add('active');
        }
      }
    }
  });
}
```

**3. Table Sorting:**

```javascript
function sortTable(tableId, columnIndex) {
  const table = document.getElementById(tableId);
  const tbody = table.querySelector('tbody');
  const rows = Array.from(tbody.querySelectorAll('tr'));
  
  rows.sort((a, b) => {
    const aValue = a.children[columnIndex].textContent;
    const bValue = b.children[columnIndex].textContent;
    return aValue.localeCompare(bValue);
  });
  
  // Clear and re-append sorted rows
  tbody.innerHTML = '';
  rows.forEach(row => tbody.appendChild(row));
}

// Add click handlers to headers
document.querySelectorAll('th').forEach((header, index) => {
  header.addEventListener('click', () => {
    const table = header.closest('table');
    sortTable(table.id, index);
  });
});
```

**4. Accordion Component:**

```javascript
function initializeAccordion() {
  const accordionHeaders = document.querySelectorAll('.accordion-header');
  
  accordionHeaders.forEach(header => {
    header.addEventListener('click', () => {
      // Find the content panel
      const content = header.nextElementSibling;
      
      // Close other panels
      const accordion = header.closest('.accordion');
      const allPanels = accordion.querySelectorAll('.accordion-content');
      const allHeaders = accordion.querySelectorAll('.accordion-header');
      
      allPanels.forEach(panel => {
        if (panel !== content) {
          panel.classList.remove('active');
        }
      });
      
      allHeaders.forEach(h => {
        if (h !== header) {
          h.classList.remove('active');
        }
      });
      
      // Toggle current panel
      header.classList.toggle('active');
      content.classList.toggle('active');
    });
  });
}
```

**Method Comparison Summary:**

```javascript
// Speed comparison (fastest to slowest):
// 1. getElementById() - O(1) hash lookup
// 2. getElementsByClassName() - Optimized by browsers
// 3. getElementsByTagName() - Optimized by browsers
// 4. querySelector() - CSS engine, slower but flexible
// 5. querySelectorAll() - CSS engine, returns all matches

// Live vs Static:
// Live (auto-updates): getElementsByClassName, getElementsByTagName, children
// Static (snapshot): querySelectorAll, childNodes (in some cases)

// When to use what:
// - getElementById(): Single element by ID (fastest)
// - querySelector(): Single element, need CSS selector flexibility
// - querySelectorAll(): Multiple elements, need CSS selector flexibility
// - getElementsByClassName(): Multiple elements by class, need live collection
// - getElementsByTagName(): Multiple elements by tag, need live collection
// - closest(): Find ancestor matching selector
// - matches(): Check if element matches selector
```

**Best Practices:**

1. **Cache DOM queries** - Don't query repeatedly in loops
2. **Use specific selectors** - More specific = faster
3. **Scope queries** - Query within a container, not whole document
4. **Use IDs when possible** - Fastest lookup method
5. **Be aware of live vs static** - Know when collections update
6. **Validate existence** - Check if element exists before using
7. **Use modern methods** - querySelector/querySelectorAll for flexibility
8. **Consider performance** - getElementById is faster than querySelector for IDs



## 87. Explain the difference between `innerHTML` and `textContent`.

### `innerHTML`
- **Purpose**: Gets or sets the HTML markup contained within an element
- **Parses HTML**: Interprets strings as HTML, creating actual DOM elements
- **Returns**: HTML tags and content as a string
- **Security Risk**: Vulnerable to XSS (Cross-Site Scripting) attacks if used with untrusted input
- **Performance**: Slower because it parses HTML and creates DOM nodes
- **Use Case**: When you need to insert or retrieve HTML structure

**Example:**
```javascript
const div = document.querySelector('.container');

// Setting innerHTML
div.innerHTML = '<strong>Bold text</strong>';
// Result: Renders as bold text

// Getting innerHTML
console.log(div.innerHTML); // "<strong>Bold text</strong>"
```

### `textContent`
- **Purpose**: Gets or sets the text content of an element and its descendants
- **No HTML Parsing**: Treats everything as plain text
- **Returns**: Only the text, stripping out all HTML tags
- **Security**: Safer - automatically escapes HTML, preventing XSS attacks
- **Performance**: Faster because it doesn't parse HTML
- **Use Case**: When working with plain text only

**Example:**
```javascript
const div = document.querySelector('.container');

// Setting textContent
div.textContent = '<strong>Bold text</strong>';
// Result: Displays literally as "<strong>Bold text</strong>"

// Getting textContent
div.innerHTML = '<strong>Hello</strong> World';
console.log(div.textContent); // "Hello World" (tags removed)
```

### Key Differences Summary

| Feature | innerHTML | textContent |
|---------|-----------|-------------|
| HTML Parsing | Yes | No |
| Security | Risky with untrusted data | Safe |
| Performance | Slower | Faster |
| Returns | HTML + text | Text only |
| Script Execution | Can execute scripts | Cannot execute scripts |

### Best Practices
- Use `textContent` when dealing with user input or displaying plain text
- Use `innerHTML` only when you need to insert trusted HTML markup
- For security-critical applications, sanitize HTML before using `innerHTML`

---

## 88. How do you handle DOM events in a memory-efficient way?

### 1. Event Delegation
Instead of attaching listeners to multiple child elements, attach a single listener to a parent element and use event bubbling.

**Inefficient Approach:**
```javascript
// Attaches multiple event listeners - memory intensive
const buttons = document.querySelectorAll('.button');
buttons.forEach(button => {
  button.addEventListener('click', handleClick);
});
```

**Efficient Approach (Event Delegation):**
```javascript
// Single event listener on parent
document.querySelector('.button-container').addEventListener('click', (e) => {
  if (e.target.matches('.button')) {
    handleClick(e);
  }
});
```

**Benefits:**
- Fewer event listeners in memory
- Works with dynamically added elements
- Better performance with large lists

### 2. Remove Event Listeners When Not Needed
Always clean up event listeners to prevent memory leaks.

```javascript
class Component {
  constructor() {
    this.handleClick = this.handleClick.bind(this);
  }

  mount() {
    this.button = document.querySelector('.btn');
    this.button.addEventListener('click', this.handleClick);
  }

  unmount() {
    // Critical: Remove listener to free memory
    this.button.removeEventListener('click', this.handleClick);
    this.button = null;
  }

  handleClick() {
    console.log('Clicked!');
  }
}
```

### 3. Use Passive Event Listeners
For scroll and touch events, use passive listeners to improve performance.

```javascript
// Passive listener - browser can optimize scrolling
document.addEventListener('scroll', handleScroll, { passive: true });

// Touch events
element.addEventListener('touchstart', handleTouch, { passive: true });
```

### 4. Debounce and Throttle High-Frequency Events
Limit how often event handlers execute for events that fire rapidly.

**Debouncing** (wait until user stops):
```javascript
function debounce(func, delay) {
  let timeoutId;
  return function(...args) {
    clearTimeout(timeoutId);
    timeoutId = setTimeout(() => func.apply(this, args), delay);
  };
}

// Usage
const searchInput = document.querySelector('#search');
searchInput.addEventListener('input', debounce((e) => {
  performSearch(e.target.value);
}, 300));
```

**Throttling** (limit execution rate):
```javascript
function throttle(func, limit) {
  let inThrottle;
  return function(...args) {
    if (!inThrottle) {
      func.apply(this, args);
      inThrottle = true;
      setTimeout(() => inThrottle = false, limit);
    }
  };
}

// Usage for scroll
window.addEventListener('scroll', throttle(() => {
  console.log('Scrolling...');
}, 100));
```

### 5. Use `once` Option
For events that should only fire once, use the `once` option instead of manually removing.

```javascript
// Automatically removes listener after first execution
button.addEventListener('click', handleClick, { once: true });

// Instead of:
function handleClick() {
  // do something
  button.removeEventListener('click', handleClick);
}
button.addEventListener('click', handleClick);
```

### 6. Avoid Anonymous Functions
Use named functions or stored references for easier cleanup.

**Bad:**
```javascript
// Cannot remove this listener later
element.addEventListener('click', () => console.log('clicked'));
```

**Good:**
```javascript
// Can be removed later
const handleClick = () => console.log('clicked');
element.addEventListener('click', handleClick);
// Later...
element.removeEventListener('click', handleClick);
```

### 7. Use AbortController for Multiple Listeners
Modern approach to remove multiple listeners at once.

```javascript
const controller = new AbortController();
const { signal } = controller;

// Add multiple listeners with the same signal
element.addEventListener('click', handleClick, { signal });
element.addEventListener('mouseover', handleHover, { signal });
window.addEventListener('resize', handleResize, { signal });

// Remove all listeners at once
controller.abort();
```

### Complete Example: Memory-Efficient List

```javascript
class EfficientList {
  constructor(containerSelector) {
    this.container = document.querySelector(containerSelector);
    this.controller = new AbortController();
    this.init();
  }

  init() {
    // Single delegated event listener
    this.container.addEventListener('click', (e) => {
      if (e.target.matches('.list-item')) {
        this.handleItemClick(e.target);
      }
      if (e.target.matches('.delete-btn')) {
        this.handleDelete(e.target);
      }
    }, { signal: this.controller.signal });

    // Throttled scroll handler
    window.addEventListener('scroll', 
      this.throttle(this.handleScroll.bind(this), 200),
      { passive: true, signal: this.controller.signal }
    );
  }

  handleItemClick(item) {
    console.log('Item clicked:', item.dataset.id);
  }

  handleDelete(btn) {
    btn.closest('.list-item').remove();
  }

  handleScroll() {
    console.log('Scrolling...');
  }

  throttle(func, limit) {
    let inThrottle;
    return function(...args) {
      if (!inThrottle) {
        func.apply(this, args);
        inThrottle = true;
        setTimeout(() => inThrottle = false, limit);
      }
    };
  }

  destroy() {
    // Clean up all event listeners at once
    this.controller.abort();
    this.container = null;
  }
}

// Usage
const list = new EfficientList('.my-list');
// When component is removed:
list.destroy();
```

### Best Practices Summary
1. **Use event delegation** for multiple similar elements
2. **Always remove listeners** when elements are destroyed
3. **Use passive listeners** for scroll/touch events
4. **Throttle/debounce** high-frequency events
5. **Use `once` option** for one-time events
6. **Use named functions** for removable listeners
7. **Use AbortController** for managing multiple listeners
8. **Avoid memory leaks** by nullifying references
9. **Profile your app** to identify memory issues




# Tooling and Build Systems (89-93)

## 89. What is npm, and how do you use it?

### What is npm?

**npm (Node Package Manager)** is the default package manager for Node.js and the world's largest software registry. It allows developers to:
- Install and manage JavaScript packages/libraries
- Share and distribute code
- Manage project dependencies
- Run scripts and automate tasks

### Key Components

1. **npm CLI** - Command-line interface tool
2. **npm Registry** - Online database of public and private packages
3. **package.json** - Configuration file that tracks dependencies

### Basic npm Commands

#### Installing npm
```bash
# npm comes bundled with Node.js
# Check if installed
npm --version
# or
npm -v
```

#### Initializing a Project
```bash
# Create a new package.json file
npm init

# Skip questionnaire (use defaults)
npm init -y
```

#### Installing Packages

**Local Installation (Project-specific):**
```bash
# Install and save to dependencies
npm install package-name
# or shorthand
npm i package-name

# Install specific version
npm install package-name@1.2.3

# Install and save to devDependencies
npm install package-name --save-dev
# or
npm i package-name -D

# Install multiple packages
npm install react react-dom axios
```

**Global Installation (System-wide):**
```bash
# Install globally
npm install -g package-name

# Example: Install nodemon globally
npm install -g nodemon
```

#### Managing Dependencies

```bash
# Install all dependencies from package.json
npm install

# Update packages
npm update

# Update specific package
npm update package-name

# Uninstall package
npm uninstall package-name

# Uninstall global package
npm uninstall -g package-name

# List installed packages
npm list

# List global packages
npm list -g --depth=0

# Check for outdated packages
npm outdated
```

#### Running Scripts

```bash
# Run script defined in package.json
npm run script-name

# Special scripts (don't need 'run')
npm start
npm test
npm stop
npm restart
```

### package.json Structure

```json
{
  "name": "my-project",
  "version": "1.0.0",
  "description": "My awesome project",
  "main": "index.js",
  "scripts": {
    "start": "node index.js",
    "dev": "nodemon index.js",
    "test": "jest",
    "build": "webpack --mode production"
  },
  "keywords": ["javascript", "example"],
  "author": "Your Name",
  "license": "MIT",
  "dependencies": {
    "express": "^4.18.2",
    "react": "^18.2.0"
  },
  "devDependencies": {
    "jest": "^29.5.0",
    "nodemon": "^2.0.22"
  }
}
```

### Understanding Semantic Versioning

```bash
# Version format: MAJOR.MINOR.PATCH (e.g., 1.2.3)

# Symbols in package.json:
"express": "4.18.2"      # Exact version
"express": "^4.18.2"     # Compatible with 4.x.x (default)
"express": "~4.18.2"     # Compatible with 4.18.x
"express": "*"           # Latest version (not recommended)
"express": ">=4.18.2"    # Greater than or equal to
```

### package-lock.json

- **Purpose**: Locks exact versions of all dependencies and sub-dependencies
- **Benefits**: Ensures consistent installations across different environments
- **Should be committed**: Yes, commit to version control

### npm Scripts Examples

```json
{
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js",
    "build": "webpack --mode production",
    "test": "jest --coverage",
    "lint": "eslint src/**/*.js",
    "format": "prettier --write \"src/**/*.js\"",
    "clean": "rm -rf dist",
    "prebuild": "npm run clean",
    "postbuild": "echo 'Build complete!'"
  }
}
```

**Running scripts:**
```bash
npm run dev
npm run build
npm test  # shorthand for npm run test
```

### Advanced npm Commands

```bash
# View package information
npm view package-name

# Search for packages
npm search keyword

# Check for security vulnerabilities
npm audit

# Fix vulnerabilities automatically
npm audit fix

# Clear npm cache
npm cache clean --force

# Login to npm registry
npm login

# Publish package
npm publish

# Create .npmignore file (like .gitignore)
```

### npx - Package Runner

```bash
# Execute package without installing
npx create-react-app my-app

# Run local package binary
npx eslint src/

# Try a package without installing
npx cowsay "Hello!"
```

### Common Use Cases

**1. Starting a React Project:**
```bash
npx create-react-app my-app
cd my-app
npm start
```

**2. Installing Development Tools:**
```bash
npm install --save-dev webpack webpack-cli babel-loader
```

**3. Managing Environment-Specific Dependencies:**
```bash
# Production dependencies
npm install express mongoose

# Development dependencies
npm install --save-dev jest eslint nodemon
```

### Best Practices

1. **Always use package-lock.json** - Commit it to version control
2. **Use semantic versioning** wisely - Understand `^` vs `~`
3. **Separate dependencies** - Use `--save-dev` for development tools
4. **Regular updates** - Keep dependencies up to date
5. **Security audits** - Run `npm audit` regularly
6. **Use .npmrc** - Configure npm behavior per project
7. **Avoid global installations** - Use npx or local installations when possible
8. **Document scripts** - Add meaningful script names in package.json

### npm vs yarn vs pnpm

| Feature | npm | yarn | pnpm |
|---------|-----|------|------|
| Speed | Good | Faster | Fastest |
| Disk Space | Standard | Standard | Efficient (shared) |
| Lock File | package-lock.json | yarn.lock | pnpm-lock.yaml |
| Workspaces | Yes | Yes | Yes |

---

## 90. Discuss the role of Webpack in modern JavaScript development.

### What is Webpack?

**Webpack** is a static module bundler for modern JavaScript applications. It processes your application's modules, analyzes dependencies, and bundles them into optimized files for the browser.

### Core Concepts

#### 1. Entry Point
Where Webpack starts building the dependency graph.

```javascript
// webpack.config.js
module.exports = {
  entry: './src/index.js'
  // Or multiple entry points
  // entry: {
  //   app: './src/app.js',
  //   admin: './src/admin.js'
  // }
};
```

#### 2. Output
Where to emit the bundled files.

```javascript
const path = require('path');

module.exports = {
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
    // Or dynamic names
    // filename: '[name].[contenthash].js'
  }
};
```

#### 3. Loaders
Transform files before they're added to the bundle (e.g., transpile TypeScript, process CSS).

```javascript
module.exports = {
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: 'babel-loader'
      },
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader']
      },
      {
        test: /\.(png|jpg|gif|svg)$/,
        type: 'asset/resource'
      }
    ]
  }
};
```

#### 4. Plugins
Extend Webpack's capabilities (e.g., optimize bundles, inject HTML).

```javascript
const HtmlWebpackPlugin = require('html-webpack-plugin');
const MiniCssExtractPlugin = require('mini-css-extract-plugin');

module.exports = {
  plugins: [
    new HtmlWebpackPlugin({
      template: './src/index.html'
    }),
    new MiniCssExtractPlugin({
      filename: '[name].[contenthash].css'
    })
  ]
};
```

### Complete Webpack Configuration Example

```javascript
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const MiniCssExtractPlugin = require('mini-css-extract-plugin');
const TerserPlugin = require('terser-webpack-plugin');

module.exports = {
  // Mode: development, production, or none
  mode: 'production',

  // Entry point
  entry: './src/index.js',

  // Output configuration
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: '[name].[contenthash].js',
    clean: true // Clean dist folder before build
  },

  // Module loaders
  module: {
    rules: [
      // JavaScript/JSX
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['@babel/preset-env', '@babel/preset-react']
          }
        }
      },
      // CSS
      {
        test: /\.css$/,
        use: [MiniCssExtractPlugin.loader, 'css-loader', 'postcss-loader']
      },
      // SCSS/SASS
      {
        test: /\.scss$/,
        use: [MiniCssExtractPlugin.loader, 'css-loader', 'sass-loader']
      },
      // Images
      {
        test: /\.(png|jpg|jpeg|gif|svg)$/,
        type: 'asset/resource'
      },
      // Fonts
      {
        test: /\.(woff|woff2|eot|ttf|otf)$/,
        type: 'asset/resource'
      }
    ]
  },

  // Plugins
  plugins: [
    new HtmlWebpackPlugin({
      template: './src/index.html',
      minify: true
    }),
    new MiniCssExtractPlugin({
      filename: '[name].[contenthash].css'
    })
  ],

  // Optimization
  optimization: {
    minimize: true,
    minimizer: [new TerserPlugin()],
    splitChunks: {
      chunks: 'all',
      cacheGroups: {
        vendor: {
          test: /[\\/]node_modules[\\/]/,
          name: 'vendors',
          priority: 10
        }
      }
    }
  },

  // Development server
  devServer: {
    static: './dist',
    port: 3000,
    hot: true,
    open: true
  },

  // Source maps
  devtool: 'source-map',

  // Resolve extensions
  resolve: {
    extensions: ['.js', '.jsx', '.json'],
    alias: {
      '@': path.resolve(__dirname, 'src')
    }
  }
};
```

### Key Features and Benefits

#### 1. **Module Bundling**
Combines multiple JavaScript files into one or more bundles.

```javascript
// Before Webpack
<script src="module1.js"></script>
<script src="module2.js"></script>
<script src="module3.js"></script>

// After Webpack
<script src="bundle.js"></script>
```

#### 2. **Code Splitting**
Split code into chunks that can be loaded on demand.

```javascript
// Dynamic import
button.addEventListener('click', async () => {
  const module = await import('./heavy-module.js');
  module.doSomething();
});

// Route-based splitting (React)
const Home = lazy(() => import('./pages/Home'));
const About = lazy(() => import('./pages/About'));
```

#### 3. **Tree Shaking**
Eliminates unused code from bundles (dead code elimination).

```javascript
// utils.js
export const add = (a, b) => a + b;
export const multiply = (a, b) => a * b; // Not used

// main.js
import { add } from './utils';
console.log(add(2, 3));

// Webpack removes 'multiply' from bundle
```

#### 4. **Hot Module Replacement (HMR)**
Updates modules in the browser without full page reload during development.

```javascript
// webpack.config.js
devServer: {
  hot: true
}

// In your code
if (module.hot) {
  module.hot.accept('./module.js', () => {
    console.log('Module updated!');
  });
}
```

#### 5. **Asset Management**
Handle images, fonts, and other assets.

```javascript
// Import assets directly
import logo from './logo.png';
import './styles.css';

// Use in code
img.src = logo;
```

#### 6. **Environment Variables**
Inject environment-specific values.

```javascript
const webpack = require('webpack');

module.exports = {
  plugins: [
    new webpack.DefinePlugin({
      'process.env.NODE_ENV': JSON.stringify('production'),
      'process.env.API_URL': JSON.stringify('https://api.example.com')
    })
  ]
};
```

### Common Loaders

```bash
# JavaScript
npm install babel-loader @babel/core @babel/preset-env

# CSS
npm install style-loader css-loader sass-loader

# TypeScript
npm install ts-loader typescript

# Images
npm install file-loader url-loader

# PostCSS
npm install postcss-loader autoprefixer
```

### Common Plugins

```bash
# HTML generation
npm install html-webpack-plugin

# CSS extraction
npm install mini-css-extract-plugin

# Bundle analysis
npm install webpack-bundle-analyzer

# Environment variables
npm install dotenv-webpack

# Clean dist folder
npm install clean-webpack-plugin
```

### Development vs Production

**Development Mode:**
```javascript
module.exports = {
  mode: 'development',
  devtool: 'eval-source-map', // Fast source maps
  devServer: {
    hot: true,
    port: 3000
  }
};
```

**Production Mode:**
```javascript
module.exports = {
  mode: 'production',
  devtool: 'source-map', // Slower but accurate
  optimization: {
    minimize: true,
    splitChunks: { chunks: 'all' }
  },
  performance: {
    hints: 'warning',
    maxAssetSize: 244000,
    maxEntrypointSize: 244000
  }
};
```

### Role in Modern Development

1. **ES6+ Support** - Transpile modern JavaScript for older browsers
2. **Module System** - Use ES6 imports/exports everywhere
3. **Asset Pipeline** - Manage all assets (JS, CSS, images, fonts)
4. **Performance** - Optimize bundles with minification, compression
5. **Development Experience** - Hot reload, fast rebuilds
6. **Framework Integration** - Works with React, Vue, Angular
7. **Code Splitting** - Lazy load code for better performance
8. **Polyfills** - Automatically add browser compatibility

### Webpack Alternatives

- **Vite** - Faster, uses native ES modules in dev
- **Parcel** - Zero-config bundler
- **Rollup** - Better for libraries
- **esbuild** - Extremely fast
- **Turbopack** - Next-generation bundler by Vercel

---

## 91. What is a source map?

### Definition

A **source map** is a file that maps minified/transpiled code back to the original source code. It allows developers to debug production code as if they were working with the original, readable source files.

### Why Source Maps Are Needed

**Problem:** Modern JavaScript goes through multiple transformations:

```javascript
// Original ES6+ code (what you write)
const greet = (name) => {
  console.log(`Hello, ${name}!`);
};
greet('World');

// After bundling and minification (what browser runs)
function n(e){console.log("Hello, "+e+"!")}n("World");
```

**Without source maps:** Debugging shows only minified code  
**With source maps:** Debugging shows original source code

### How Source Maps Work

```
Original File          Source Map              Minified File
    ↓                      ↓                         ↓
index.js  ──────→  index.js.map  ←──────  index.min.js
(readable)        (mapping data)          (minified)
```

The source map file contains:
- **Mappings** - Connections between minified and original code positions
- **Sources** - Original file names
- **SourcesContent** - Original source code (optional)
- **Names** - Original variable/function names

### Source Map Structure

```json
{
  "version": 3,
  "file": "bundle.min.js",
  "sources": [
    "src/index.js",
    "src/utils.js"
  ],
  "sourcesContent": [
    "const greet = (name) => {...}",
    "export const add = (a, b) => a + b;"
  ],
  "names": ["greet", "name", "add", "a", "b"],
  "mappings": "AAAA,MAAMA,EAAQ,CAACC,IACbC,QAAQC,IAAI..."
}
```

### Enabling Source Maps

#### Webpack Configuration

```javascript
module.exports = {
  devtool: 'source-map', // Various options available
  
  // Other options:
  // devtool: 'eval-source-map'        // Fast rebuild, good for dev
  // devtool: 'cheap-source-map'       // Faster, less accurate
  // devtool: 'inline-source-map'      // Embedded in bundle
  // devtool: 'hidden-source-map'      // No reference in bundle
  // devtool: 'nosources-source-map'   // No source content
};
```

#### Different Source Map Types

| Type | Build Speed | Rebuild Speed | Production | Quality |
|------|-------------|---------------|------------|---------|
| `eval` | +++++ | +++++ | No | Generated code |
| `eval-source-map` | -- | + | No | Original source |
| `cheap-source-map` | + | ++ | Yes | Transformed code |
| `source-map` | -- | -- | Yes | Original source |
| `hidden-source-map` | -- | -- | Yes | Original source (hidden) |
| `nosources-source-map` | -- | -- | Yes | Line/column only |

#### Babel Configuration

```json
// .babelrc
{
  "presets": ["@babel/preset-env"],
  "sourceMaps": true
}
```

#### TypeScript Configuration

```json
// tsconfig.json
{
  "compilerOptions": {
    "sourceMap": true,
    "inlineSourceMap": false,
    "inlineSources": false
  }
}
```

#### Minification with Source Maps

```javascript
// Using Terser (Webpack 5)
const TerserPlugin = require('terser-webpack-plugin');

module.exports = {
  optimization: {
    minimize: true,
    minimizer: [
      new TerserPlugin({
        sourceMap: true
      })
    ]
  }
};
```

### Using Source Maps in Browsers

#### Browser DevTools

**Chrome/Edge:**
1. Open DevTools → Settings → Preferences
2. Enable "Enable JavaScript source maps"
3. Enable "Enable CSS source maps"

**Firefox:**
1. Open DevTools → Settings (gear icon)
2. Check "Enable Source Maps"

**When debugging:**
```javascript
// Minified code shows as:
function a(b){console.log(b)}

// With source maps, you see:
const greet = (name) => {
  console.log(name);  // ← Set breakpoints here!
};
```

### Source Map Comment

Browsers discover source maps through a comment at the end of the file:

```javascript
// At the end of bundle.min.js
//# sourceMappingURL=bundle.min.js.map

// Or inline (not recommended for production):
//# sourceMappingURL=data:application/json;base64,eyJ2ZXJzaW9u...
```

### Security Considerations

#### Production Source Maps

**Option 1: Don't include in production**
```javascript
module.exports = {
  devtool: process.env.NODE_ENV === 'production' ? false : 'eval-source-map'
};
```

**Option 2: Use hidden source maps**
```javascript
module.exports = {
  devtool: 'hidden-source-map' // No reference in bundle
};
```
- Source map is generated but not referenced
- Upload to error tracking service (Sentry, Rollbar)
- Not accessible to public

**Option 3: Restrict access**
```nginx
# Nginx configuration
location ~ \.map$ {
  deny all;
  # Or allow only internal IPs
  # allow 10.0.0.0/8;
  # deny all;
}
```

### Error Tracking with Source Maps

**Sentry Integration:**
```javascript
// Upload source maps to Sentry
const SentryWebpackPlugin = require('@sentry/webpack-plugin');

module.exports = {
  devtool: 'hidden-source-map',
  plugins: [
    new SentryWebpackPlugin({
      include: './dist',
      ignore: ['node_modules', 'webpack.config.js'],
      release: process.env.RELEASE
    })
  ]
};
```

### Benefits of Source Maps

1. **Debugging** - See original code in browser DevTools
2. **Stack Traces** - Get readable error stack traces
3. **Breakpoints** - Set breakpoints in original source
4. **Performance Monitoring** - Track performance with proper function names
5. **Error Tracking** - Services like Sentry can show original code locations

### Best Practices

```javascript
// Development
module.exports = {
  mode: 'development',
  devtool: 'eval-cheap-module-source-map', // Fast, good quality
};

// Production
module.exports = {
  mode: 'production',
  devtool: 'source-map', // or 'hidden-source-map'
  // Upload source maps to error tracking service
  // Don't deploy .map files to public
};
```

### Common Issues and Solutions

**Issue: Source maps not loading**
```javascript
// Solution: Ensure correct path
output: {
  sourceMapFilename: '[file].map',
  publicPath: '/'
}
```

**Issue: Large source map files**
```javascript
// Solution: Exclude source content
devtool: 'nosources-source-map'
```

**Issue: Debugging shows wrong lines**
```javascript
// Solution: Use accurate source maps
devtool: 'source-map' // Not 'cheap-source-map'
```

### Checking Source Maps

```bash
# View source map
cat dist/bundle.js.map | jq .

# Validate source map
npx source-map-validator dist/bundle.js
```

### Example: Complete Setup

```javascript
// webpack.config.js
const path = require('path');

module.exports = (env, argv) => {
  const isDevelopment = argv.mode === 'development';

  return {
    mode: argv.mode,
    entry: './src/index.js',
    output: {
      path: path.resolve(__dirname, 'dist'),
      filename: '[name].[contenthash].js',
      sourceMapFilename: '[file].map'
    },
    devtool: isDevelopment 
      ? 'eval-cheap-module-source-map'  // Fast for dev
      : 'hidden-source-map',            // Secure for prod
    module: {
      rules: [
        {
          test: /\.js$/,
          exclude: /node_modules/,
          use: {
            loader: 'babel-loader',
            options: {
              sourceMaps: true
            }
          }
        }
      ]
    }
  };
};
```

Source maps are essential for maintaining developer productivity while still benefiting from minified, optimized production code.



## 92. How do you use ESLint for maintaining JavaScript code quality?

### What is ESLint?

**ESLint** is a static code analysis tool for identifying and fixing problems in JavaScript code. It helps enforce coding standards, catch bugs early, and maintain consistent code style across teams.

### Installation and Setup

#### Basic Installation

```bash
# Install ESLint locally (recommended)
npm install --save-dev eslint

# Or install globally
npm install -g eslint

# Initialize ESLint configuration
npx eslint --init
```

#### Interactive Setup

When you run `eslint --init`, you'll be asked:

```bash
? How would you like to use ESLint?
  > To check syntax and find problems
  > To check syntax, find problems, and enforce code style

? What type of modules does your project use?
  > JavaScript modules (import/export)
  > CommonJS (require/exports)

? Which framework does your project use?
  > React
  > Vue.js
  > None of these

? Does your project use TypeScript?
  > No / Yes

? Where does your code run?
  > Browser
  > Node

? What format do you want your config file to be in?
  > JavaScript
  > YAML
  > JSON
```

### Configuration Files

#### .eslintrc.js (Most Common)

```javascript
module.exports = {
  // Environment settings
  env: {
    browser: true,
    es2021: true,
    node: true,
    jest: true
  },

  // Extends existing configurations
  extends: [
    'eslint:recommended',
    'plugin:react/recommended',
    'plugin:@typescript-eslint/recommended',
    'prettier' // Disable conflicting rules with Prettier
  ],

  // Parser options
  parserOptions: {
    ecmaVersion: 'latest',
    sourceType: 'module',
    ecmaFeatures: {
      jsx: true
    }
  },

  // Plugins
  plugins: [
    'react',
    'react-hooks',
    '@typescript-eslint'
  ],

  // Custom rules
  rules: {
    // Possible errors
    'no-console': 'warn',
    'no-debugger': 'error',
    'no-duplicate-imports': 'error',
    
    // Best practices
    'eqeqeq': ['error', 'always'],
    'no-var': 'error',
    'prefer-const': 'error',
    'prefer-arrow-callback': 'warn',
    
    // Stylistic
    'semi': ['error', 'always'],
    'quotes': ['error', 'single'],
    'indent': ['error', 2],
    'comma-dangle': ['error', 'never'],
    
    // React specific
    'react/prop-types': 'off',
    'react/react-in-jsx-scope': 'off',
    'react-hooks/rules-of-hooks': 'error',
    'react-hooks/exhaustive-deps': 'warn'
  },

  // Settings for plugins
  settings: {
    react: {
      version: 'detect'
    }
  },

  // Override rules for specific files
  overrides: [
    {
      files: ['*.test.js', '*.spec.js'],
      rules: {
        'no-console': 'off'
      }
    }
  ]
};
```

#### .eslintrc.json

```json
{
  "env": {
    "browser": true,
    "es2021": true
  },
  "extends": "eslint:recommended",
  "parserOptions": {
    "ecmaVersion": "latest",
    "sourceType": "module"
  },
  "rules": {
    "semi": ["error", "always"],
    "quotes": ["error", "single"]
  }
}
```

#### package.json Configuration

```json
{
  "eslintConfig": {
    "extends": ["react-app"],
    "rules": {
      "no-console": "warn"
    }
  }
}
```

### Rule Levels

```javascript
rules: {
  // "off" or 0 - Disable the rule
  'no-unused-vars': 'off',
  
  // "warn" or 1 - Warning (doesn't affect exit code)
  'no-console': 'warn',
  
  // "error" or 2 - Error (exit code 1)
  'no-debugger': 'error',
  
  // With options
  'quotes': ['error', 'single', { 'allowTemplateLiterals': true }],
  'max-len': ['warn', { 'code': 100, 'ignoreUrls': true }]
}
```

### Running ESLint

#### Command Line

```bash
# Lint all JavaScript files in src directory
npx eslint src/

# Lint specific file
npx eslint src/index.js

# Lint with automatic fixing
npx eslint src/ --fix

# Lint and output to file
npx eslint src/ -o report.txt

# Lint with specific format
npx eslint src/ --format stylish
npx eslint src/ --format json
```

#### npm Scripts

```json
{
  "scripts": {
    "lint": "eslint src/",
    "lint:fix": "eslint src/ --fix",
    "lint:report": "eslint src/ -o eslint-report.json --format json"
  }
}
```

**Usage:**
```bash
npm run lint
npm run lint:fix
```

### Popular ESLint Configurations

#### 1. Airbnb Style Guide

```bash
# Install
npx install-peerdeps --dev eslint-config-airbnb

# Configuration
module.exports = {
  extends: ['airbnb', 'airbnb/hooks']
};
```

#### 2. Standard JS

```bash
# Install
npm install --save-dev eslint-config-standard

# Configuration
module.exports = {
  extends: 'standard'
};
```

#### 3. Google Style Guide

```bash
# Install
npm install --save-dev eslint-config-google

# Configuration
module.exports = {
  extends: 'google'
};
```

#### 4. React-specific

```bash
# Install
npm install --save-dev eslint-plugin-react eslint-plugin-react-hooks

# Configuration
module.exports = {
  extends: [
    'plugin:react/recommended',
    'plugin:react-hooks/recommended'
  ]
};
```

### Common ESLint Plugins

```bash
# React
npm install --save-dev eslint-plugin-react

# TypeScript
npm install --save-dev @typescript-eslint/parser @typescript-eslint/eslint-plugin

# Import/Export validation
npm install --save-dev eslint-plugin-import

# JSX Accessibility
npm install --save-dev eslint-plugin-jsx-a11y

# Node.js
npm install --save-dev eslint-plugin-node

# Jest
npm install --save-dev eslint-plugin-jest

# Security
npm install --save-dev eslint-plugin-security
```

### Ignoring Files

#### .eslintignore

```
# Dependencies
node_modules/
bower_components/

# Build outputs
dist/
build/
*.min.js

# Configuration
*.config.js
webpack.config.js

# Test coverage
coverage/

# Specific files
src/legacy/**/*.js
```

#### Inline Comments

```javascript
// Disable for entire file
/* eslint-disable */

// Disable specific rule for file
/* eslint-disable no-console */

// Disable for next line
// eslint-disable-next-line no-console
console.log('Debug message');

// Disable for current line
console.log('Debug'); // eslint-disable-line no-console

// Disable multiple rules
// eslint-disable-next-line no-console, no-alert
console.log('test');
alert('test');

// Re-enable rules
/* eslint-enable no-console */
```

### Integration with Development Tools

#### VS Code Integration

**Install Extension:**
- Search for "ESLint" by Microsoft
- Install extension

**settings.json:**
```json
{
  "eslint.enable": true,
  "eslint.autoFixOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "eslint.validate": [
    "javascript",
    "javascriptreact",
    "typescript",
    "typescriptreact"
  ]
}
```

#### Webpack Integration

```bash
npm install --save-dev eslint-webpack-plugin
```

```javascript
const ESLintPlugin = require('eslint-webpack-plugin');

module.exports = {
  plugins: [
    new ESLintPlugin({
      extensions: ['js', 'jsx'],
      fix: true,
      emitWarning: true
    })
  ]
};
```

#### Git Hooks with Husky and lint-staged

```bash
# Install dependencies
npm install --save-dev husky lint-staged

# Initialize husky
npx husky-init
npm install
```

**package.json:**
```json
{
  "lint-staged": {
    "*.{js,jsx,ts,tsx}": [
      "eslint --fix",
      "git add"
    ]
  },
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged"
    }
  }
}
```

**Alternative (Husky v6+):**
```bash
# Create pre-commit hook
npx husky add .husky/pre-commit "npx lint-staged"
```

### Custom Rules

#### Creating a Custom Rule

```javascript
// eslint-rules/no-console-log.js
module.exports = {
  meta: {
    type: 'suggestion',
    docs: {
      description: 'Disallow console.log statements',
      category: 'Best Practices'
    },
    fixable: 'code',
    schema: []
  },
  create(context) {
    return {
      CallExpression(node) {
        if (
          node.callee.object &&
          node.callee.object.name === 'console' &&
          node.callee.property.name === 'log'
        ) {
          context.report({
            node,
            message: 'Unexpected console.log statement.',
            fix(fixer) {
              return fixer.remove(node);
            }
          });
        }
      }
    };
  }
};
```

**Using custom rule:**
```javascript
// .eslintrc.js
module.exports = {
  rules: {
    'local/no-console-log': 'error'
  },
  plugins: ['local'],
  // Load custom rules
  rulePaths: ['./eslint-rules']
};
```

### ESLint + Prettier Integration

```bash
# Install Prettier and ESLint config
npm install --save-dev prettier eslint-config-prettier eslint-plugin-prettier
```

**.eslintrc.js:**
```javascript
module.exports = {
  extends: [
    'eslint:recommended',
    'prettier' // Turns off ESLint rules that conflict with Prettier
  ],
  plugins: ['prettier'],
  rules: {
    'prettier/prettier': 'error'
  }
};
```

**.prettierrc:**
```json
{
  "semi": true,
  "singleQuote": true,
  "trailingComma": "es5",
  "tabWidth": 2,
  "printWidth": 80
}
```

### Complete Example: React Project Setup

```bash
# Install dependencies
npm install --save-dev \
  eslint \
  eslint-config-airbnb \
  eslint-plugin-react \
  eslint-plugin-react-hooks \
  eslint-plugin-import \
  eslint-plugin-jsx-a11y \
  prettier \
  eslint-config-prettier \
  eslint-plugin-prettier
```

**.eslintrc.js:**
```javascript
module.exports = {
  env: {
    browser: true,
    es2021: true,
    node: true,
    jest: true
  },
  extends: [
    'airbnb',
    'airbnb/hooks',
    'plugin:react/recommended',
    'plugin:jsx-a11y/recommended',
    'prettier'
  ],
  parserOptions: {
    ecmaVersion: 'latest',
    sourceType: 'module',
    ecmaFeatures: {
      jsx: true
    }
  },
  plugins: ['react', 'react-hooks', 'jsx-a11y', 'prettier'],
  rules: {
    'prettier/prettier': 'error',
    'react/react-in-jsx-scope': 'off',
    'react/prop-types': 'off',
    'no-console': 'warn',
    'import/prefer-default-export': 'off'
  },
  settings: {
    react: {
      version: 'detect'
    }
  }
};
```

**package.json scripts:**
```json
{
  "scripts": {
    "lint": "eslint src/",
    "lint:fix": "eslint src/ --fix",
    "format": "prettier --write \"src/**/*.{js,jsx,json,css,md}\""
  }
}
```

### Best Practices

1. **Start with a popular style guide** (Airbnb, Standard, Google)
2. **Use .eslintignore** to exclude generated/vendor files
3. **Enable auto-fix in your editor** for instant feedback
4. **Run ESLint in CI/CD** to enforce standards
5. **Use lint-staged** to lint only changed files
6. **Combine with Prettier** for formatting
7. **Document custom rules** and exceptions
8. **Update regularly** to get new rules and fixes
9. **Educate your team** on ESLint rules
10. **Don't disable rules** without good reason

### Common ESLint Errors and Fixes

```javascript
// Error: 'React' must be in scope when using JSX
// Fix: Import React or use React 17+ JSX transform
import React from 'react';

// Error: Missing semicolon
// Fix: Add semicolon or configure rule
const x = 5;

// Error: Unexpected console statement
// Fix: Remove or disable for that line
// eslint-disable-next-line no-console
console.log('Debug info');

// Error: Prefer arrow callback
// Fix: Use arrow function
array.map(item => item * 2);

// Error: 'x' is assigned a value but never used
// Fix: Remove unused variable or use it
const x = getValue(); // Remove if unused
```

---

## 93. What is continuous integration/continuous deployment (CI/CD) in the context of JS development?

### What is CI/CD?

**Continuous Integration (CI)** and **Continuous Deployment/Delivery (CD)** are practices that automate the process of testing, building, and deploying code changes.

#### Continuous Integration (CI)
- Automatically test code when changes are pushed
- Merge code frequently (multiple times per day)
- Detect integration issues early
- Ensure code quality through automated checks

#### Continuous Deployment (CD)
- **Continuous Delivery**: Automatically prepare code for release (manual deploy)
- **Continuous Deployment**: Automatically deploy to production (no manual intervention)

### CI/CD Pipeline Flow

```
Code Push → CI Triggers → Run Tests → Build → Deploy
    ↓
 GitHub      Jenkins      Jest/      Webpack   Production
 GitLab      CircleCI     Mocha      Rollup    Staging
 Bitbucket   Travis CI    Cypress    Vite      Development
```

### Benefits in JavaScript Development

1. **Early Bug Detection** - Catch errors before production
2. **Faster Releases** - Automate repetitive tasks
3. **Consistent Builds** - Same process every time
4. **Better Code Quality** - Automated linting and testing
5. **Reduced Risk** - Small, incremental changes
6. **Team Collaboration** - Shared standards and processes

### Popular CI/CD Platforms

#### 1. GitHub Actions
- Native to GitHub
- Free for public repos
- YAML configuration

#### 2. GitLab CI/CD
- Built into GitLab
- Runner-based system
- Docker support

#### 3. CircleCI
- Cloud-based
- Docker-native
- Great caching

#### 4. Travis CI
- Popular for open source
- Simple YAML config
- Good GitHub integration

#### 5. Jenkins
- Self-hosted
- Highly customizable
- Extensive plugin ecosystem

### GitHub Actions Example

#### Basic Node.js CI Pipeline

```yaml
# .github/workflows/ci.yml
name: Node.js CI

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest

    strategy:
      matrix:
        node-version: [16.x, 18.x, 20.x]

    steps:
    - name: Checkout code
      uses: actions/checkout@v3

    - name: Setup Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v3
      with:
        node-version: ${{ matrix.node-version }}
        cache: 'npm'

    - name: Install dependencies
      run: npm ci

    - name: Run linter
      run: npm run lint

    - name: Run tests
      run: npm test

    - name: Check code coverage
      run: npm run test:coverage

    - name: Upload coverage to Codecov
      uses: codecov/codecov-action@v3
      with:
        files: ./coverage/lcov.info
```

#### Full CI/CD Pipeline with Deployment

```yaml
# .github/workflows/deploy.yml
name: Build and Deploy

on:
  push:
    branches: [ main ]

jobs:
  build-and-test:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3

    - name: Setup Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '18.x'
        cache: 'npm'

    - name: Install dependencies
      run: npm ci

    - name: Run ESLint
      run: npm run lint

    - name: Run unit tests
      run: npm run test:unit

    - name: Run integration tests
      run: npm run test:integration

    - name: Build application
      run: npm run build
      env:
        NODE_ENV: production

    - name: Archive production artifacts
      uses: actions/upload-artifact@v3
      with:
        name: dist
        path: dist/

  deploy-staging:
    needs: build-and-test
    runs-on: ubuntu-latest
    environment: staging

    steps:
    - name: Download artifacts
      uses: actions/download-artifact@v3
      with:
        name: dist
        path: dist/

    - name: Deploy to staging
      run: |
        npm install -g netlify-cli
        netlify deploy --dir=dist --prod
      env:
        NETLIFY_AUTH_TOKEN: ${{ secrets.NETLIFY_AUTH_TOKEN }}
        NETLIFY_SITE_ID: ${{ secrets.NETLIFY_SITE_ID }}

  deploy-production:
    needs: deploy-staging
    runs-on: ubuntu-latest
    environment: production
    if: github.ref == 'refs/heads/main'

    steps:
    - name: Download artifacts
      uses: actions/download-artifact@v3
      with:
        name: dist
        path: dist/

    - name: Deploy to production
      run: |
        npm install -g vercel
        vercel --prod --token=${{ secrets.VERCEL_TOKEN }}
```

### GitLab CI/CD Example

```yaml
# .gitlab-ci.yml
image: node:18

stages:
  - install
  - test
  - build
  - deploy

cache:
  paths:
    - node_modules/

install_dependencies:
  stage: install
  script:
    - npm ci
  artifacts:
    paths:
      - node_modules/

lint:
  stage: test
  script:
    - npm run lint

unit_tests:
  stage: test
  script:
    - npm run test:unit
  coverage: '/Statements\s*:\s*(\d+\.\d+)%/'
  artifacts:
    reports:
      coverage_report:
        coverage_format: cobertura
        path: coverage/cobertura-coverage.xml

e2e_tests:
  stage: test
  script:
    - npm run test:e2e
  allow_failure: true

build:
  stage: build
  script:
    - npm run build
  artifacts:
    paths:
      - dist/
    expire_in: 1 week

deploy_staging:
  stage: deploy
  script:
    - npm run deploy:staging
  environment:
    name: staging
    url: https://staging.example.com
  only:
    - develop

deploy_production:
  stage: deploy
  script:
    - npm run deploy:production
  environment:
    name: production
    url: https://example.com
  only:
    - main
  when: manual
```

### CircleCI Example

```yaml
# .circleci/config.yml
version: 2.1

orbs:
  node: circleci/node@5.0.0

jobs:
  test:
    docker:
      - image: cimg/node:18.0
    steps:
      - checkout
      - node/install-packages:
          pkg-manager: npm
      - run:
          name: Run tests
          command: npm test
      - run:
          name: Run linter
          command: npm run lint
      - store_test_results:
          path: test-results
      - store_artifacts:
          path: coverage

  build:
    docker:
      - image: cimg/node:18.0
    steps:
      - checkout
      - node/install-packages
      - run:
          name: Build application
          command: npm run build
      - persist_to_workspace:
          root: .
          paths:
            - dist

  deploy:
    docker:
      - image: cimg/node:18.0
    steps:
      - attach_workspace:
          at: .
      - run:
          name: Deploy to production
          command: |
            npm install -g netlify-cli
            netlify deploy --prod --dir=dist

workflows:
  test-build-deploy:
    jobs:
      - test
      - build:
          requires:
            - test
      - deploy:
          requires:
            - build
          filters:
            branches:
              only: main
```

### Package.json Scripts for CI/CD

```json
{
  "scripts": {
    "test": "jest",
    "test:unit": "jest --testPathPattern=unit",
    "test:integration": "jest --testPathPattern=integration",
    "test:e2e": "cypress run",
    "test:coverage": "jest --coverage",
    "test:watch": "jest --watch",
    
    "lint": "eslint src/",
    "lint:fix": "eslint src/ --fix",
    "format": "prettier --write \"src/**/*.{js,jsx,json,css}\"",
    "format:check": "prettier --check \"src/**/*.{js,jsx,json,css}\"",
    
    "build": "webpack --mode production",
    "build:staging": "webpack --mode production --env staging",
    "build:analyze": "webpack --mode production --analyze",
    
    "deploy:staging": "node scripts/deploy-staging.js",
    "deploy:production": "node scripts/deploy-production.js",
    
    "ci": "npm run lint && npm run test && npm run build",
    "precommit": "lint-staged",
    "prepare": "husky install"
  }
}
```

### Docker Integration

#### Dockerfile for Node.js App

```dockerfile
# Multi-stage build
FROM node:18-alpine AS builder

WORKDIR /app

COPY package*.json ./
RUN npm ci --only=production

COPY . .
RUN npm run build

# Production image
FROM node:18-alpine

WORKDIR /app

COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules ./node_modules
COPY package*.json ./

EXPOSE 3000

USER node

CMD ["node", "dist/server.js"]
```

#### Docker Compose for Testing

```yaml
# docker-compose.test.yml
version: '3.8'

services:
  app:
    build: .
    environment:
      - NODE_ENV=test
      - DATABASE_URL=postgresql://test:test@db:5432/testdb
    depends_on:
      - db
    command: npm test

  db:
    image: postgres:14
    environment:
      POSTGRES_USER: test
      POSTGRES_PASSWORD: test
      POSTGRES_DB: testdb
```

### Environment Variables and Secrets

#### GitHub Actions Secrets

```yaml
steps:
  - name: Deploy
    env:
      API_KEY: ${{ secrets.API_KEY }}
      DATABASE_URL: ${{ secrets.DATABASE_URL }}
      SENTRY_DSN: ${{ secrets.SENTRY_DSN }}
    run: npm run deploy
```

#### .env Files for Different Environments

```bash
# .env.development
NODE_ENV=development
API_URL=http://localhost:3000
DEBUG=true

# .env.staging
NODE_ENV=staging
API_URL=https://staging-api.example.com
DEBUG=false

# .env.production
NODE_ENV=production
API_URL=https://api.example.com
DEBUG=false
```

### Testing in CI/CD

```yaml
# Parallel test execution
test:
  strategy:
    matrix:
      test-type: [unit, integration, e2e]
  steps:
    - run: npm run test:${{ matrix.test-type }}

# Browser testing
e2e-tests:
  strategy:
    matrix:
      browser: [chrome, firefox, safari]
  steps:
    - run: npm run test:e2e -- --browser=${{ matrix.browser }}
```

### Caching Strategies

```yaml
# GitHub Actions caching
- name: Cache node modules
  uses: actions/cache@v3
  with:
    path: |
      node_modules
      ~/.npm
    key: ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}
    restore-keys: |
      ${{ runner.os }}-node-
```

### Notifications and Monitoring

```yaml
# Slack notification on failure
- name: Notify Slack
  if: failure()
  uses: 8398a7/action-slack@v3
  with:
    status: ${{ job.status }}
    text: 'Build failed!'
    webhook_url: ${{ secrets.SLACK_WEBHOOK }}

# Email notification
- name: Send email
  if: failure()
  uses: dawidd6/action-send-mail@v3
  with:
    server_address: smtp.gmail.com
    server_port: 465
    username: ${{ secrets.MAIL_USERNAME }}
    password: ${{ secrets.MAIL_PASSWORD }}
    subject: Build Failed - ${{ github.repository }}
    body: Commit ${{ github.sha }} failed
    to: team@example.com
```

### Best Practices

1. **Keep pipelines fast** - Run tests in parallel, use caching
2. **Fail fast** - Run quick checks first (linting) before slow tests
3. **Use matrix builds** - Test across multiple Node.js versions
4. **Separate concerns** - Different jobs for test, build, deploy
5. **Environment parity** - Make CI environment similar to production
6. **Security** - Never commit secrets, use environment variables
7. **Automated rollbacks** - Have a plan for failed deployments
8. **Monitor pipelines** - Track build times and success rates
9. **Documentation** - Document your CI/CD process
10. **Incremental adoption** - Start simple, add complexity as needed

### Common CI/CD Workflow

```
Developer commits code
         ↓
    Git push to repository
         ↓
    CI/CD pipeline triggered
         ↓
    ┌─────────────────┐
    │   Code Quality  │
    │  - Linting      │
    │  - Formatting   │
    └────────┬────────┘
             ↓
    ┌─────────────────┐
    │   Run Tests     │
    │  - Unit tests   │
    │  - Integration  │
    │  - E2E tests    │
    └────────┬────────┘
             ↓
    ┌─────────────────┐
    │   Build         │
    │  - Compile      │
    │  - Bundle       │
    │  - Optimize     │
    └────────┬────────┘
             ↓
    ┌─────────────────┐
    │   Deploy        │
    │  - Staging      │
    │  - Production   │
    └─────────────────┘
```

### Deployment Strategies

**1. Blue-Green Deployment**
```yaml
- Deploy to green environment
- Run smoke tests
- Switch traffic to green
- Keep blue as rollback
```

**2. Canary Deployment**
```yaml
- Deploy to small subset of servers
- Monitor metrics
- Gradually increase traffic
- Full rollout or rollback
```

**3. Rolling Deployment**
```yaml
- Deploy to one server at a time
- Health check before next
- Continue until all updated
```

CI/CD transforms JavaScript development by automating repetitive tasks, catching bugs early, and enabling faster, more reliable releases.




# JavaScript and the Web Platform (94-97)

## 94. What is the Window object and its significance?

### What is the Window Object?

The **Window object** represents the browser's window/tab and is the **global object** in browser-based JavaScript. It serves as the top-level container for all JavaScript code running in a browser environment.

### Key Characteristics

```javascript
// Window is the global object
console.log(window); // Window object

// All global variables are properties of window
var globalVar = 'Hello';
console.log(window.globalVar); // "Hello"

// All global functions are methods of window
function greet() {
  return 'Hi';
}
console.log(window.greet()); // "Hi"

// In global scope, 'this' refers to window
console.log(this === window); // true (in browser)
```

### Window Object Properties

#### 1. Dimension and Position Properties

```javascript
// Browser window dimensions
window.innerWidth;      // Width of viewport (excludes scrollbar)
window.innerHeight;     // Height of viewport (excludes scrollbar)
window.outerWidth;      // Width of entire browser window
window.outerHeight;     // Height of entire browser window

// Window position
window.screenX;         // X coordinate from left of screen
window.screenY;         // Y coordinate from top of screen
window.scrollX;         // Horizontal scroll position
window.scrollY;         // Vertical scroll position

// Example: Get viewport dimensions
console.log(`Viewport: ${window.innerWidth}x${window.innerHeight}`);

// Example: Check if scrolled
if (window.scrollY > 100) {
  console.log('Scrolled past 100px');
}
```

#### 2. Document and Location

```javascript
// Document object
window.document;        // Reference to DOM document
window.document === document; // true

// Location object
window.location;        // Current URL information
window.location.href;   // Full URL
window.location.hostname; // Domain name
window.location.pathname; // Path
window.location.search; // Query string

// Example: Redirect
window.location.href = 'https://example.com';

// Example: Reload page
window.location.reload();

// Example: Get query parameters
const params = new URLSearchParams(window.location.search);
console.log(params.get('id'));
```

#### 3. History Object

```javascript
// Browser history
window.history.length;  // Number of entries
window.history.back();  // Go back
window.history.forward(); // Go forward
window.history.go(-2);  // Go back 2 pages

// Modern history API
window.history.pushState({page: 1}, 'Title', '/page1');
window.history.replaceState({page: 2}, 'Title', '/page2');

// Listen to history changes
window.addEventListener('popstate', (event) => {
  console.log('State:', event.state);
});
```

#### 4. Navigator Object

```javascript
// Browser information
window.navigator.userAgent;     // User agent string
window.navigator.language;      // Browser language
window.navigator.languages;     // Preferred languages
window.navigator.onLine;        // Online status
window.navigator.platform;      // Operating system
window.navigator.cookieEnabled; // Cookies enabled?

// Geolocation
navigator.geolocation.getCurrentPosition(
  (position) => {
    console.log(position.coords.latitude);
    console.log(position.coords.longitude);
  },
  (error) => console.error(error)
);

// Check if online
if (navigator.onLine) {
  console.log('Connected to internet');
} else {
  console.log('Offline');
}
```

#### 5. Screen Object

```javascript
// Screen information
window.screen.width;       // Screen width
window.screen.height;      // Screen height
window.screen.availWidth;  // Available width (minus taskbar)
window.screen.availHeight; // Available height
window.screen.colorDepth;  // Color depth (bits)
window.screen.pixelDepth;  // Pixel depth

// Example: Detect mobile screen
if (window.screen.width < 768) {
  console.log('Mobile device');
}
```

### Window Object Methods

#### 1. Alert, Confirm, and Prompt

```javascript
// Alert dialog
window.alert('This is an alert!');
alert('No need to use window prefix');

// Confirm dialog (returns boolean)
const confirmed = window.confirm('Are you sure?');
if (confirmed) {
  console.log('User confirmed');
}

// Prompt dialog (returns string or null)
const name = window.prompt('Enter your name:', 'Default Name');
if (name !== null) {
  console.log(`Hello, ${name}!`);
}
```

#### 2. Timers

```javascript
// setTimeout - Execute once after delay
const timeoutId = window.setTimeout(() => {
  console.log('Executed after 2 seconds');
}, 2000);

// Clear timeout
window.clearTimeout(timeoutId);

// setInterval - Execute repeatedly
const intervalId = window.setInterval(() => {
  console.log('Executed every 3 seconds');
}, 3000);

// Clear interval
window.clearInterval(intervalId);

// Example: Countdown timer
let count = 10;
const countdownId = setInterval(() => {
  console.log(count--);
  if (count < 0) {
    clearInterval(countdownId);
    console.log('Done!');
  }
}, 1000);
```

#### 3. Window Management

```javascript
// Open new window
const newWindow = window.open(
  'https://example.com',
  '_blank',
  'width=600,height=400,top=100,left=100'
);

// Close window
newWindow.close();

// Check if window is closed
if (newWindow.closed) {
  console.log('Window is closed');
}

// Focus window
window.focus();

// Blur (unfocus) window
window.blur();

// Example: Open popup
const popup = window.open('', 'popup', 'width=400,height=300');
popup.document.write('<h1>Popup Content</h1>');
```

#### 4. Scrolling

```javascript
// Scroll to coordinates
window.scrollTo(0, 500);     // Scroll to 500px from top
window.scrollTo({
  top: 500,
  left: 0,
  behavior: 'smooth'         // Smooth scrolling
});

// Scroll by amount
window.scrollBy(0, 100);     // Scroll down 100px
window.scrollBy({
  top: 100,
  behavior: 'smooth'
});

// Scroll element into view
const element = document.getElementById('section');
element.scrollIntoView({ behavior: 'smooth', block: 'start' });
```

#### 5. Frame and Window Communication

```javascript
// Parent and frames
window.parent;    // Parent window
window.top;       // Topmost window
window.self;      // Current window (same as window)
window.frames;    // Array of frames

// Post message (cross-origin communication)
// In parent window
const iframe = document.getElementById('myIframe');
iframe.contentWindow.postMessage('Hello from parent', '*');

// In iframe
window.addEventListener('message', (event) => {
  console.log('Received:', event.data);
  console.log('From:', event.origin);
  // Send response
  event.source.postMessage('Hello from iframe', event.origin);
});
```

### Window Events

```javascript
// Load event - Fires when page fully loaded
window.addEventListener('load', () => {
  console.log('Page fully loaded');
});

// DOMContentLoaded - Fires when DOM ready (faster than load)
window.addEventListener('DOMContentLoaded', () => {
  console.log('DOM ready');
});

// Resize event
window.addEventListener('resize', () => {
  console.log(`Window resized: ${window.innerWidth}x${window.innerHeight}`);
});

// Scroll event
window.addEventListener('scroll', () => {
  console.log(`Scrolled to: ${window.scrollY}`);
});

// Before unload - Warn before leaving page
window.addEventListener('beforeunload', (event) => {
  event.preventDefault();
  event.returnValue = ''; // Chrome requires this
  return 'Are you sure you want to leave?';
});

// Unload - Clean up before leaving
window.addEventListener('unload', () => {
  // Send analytics, clean up
  navigator.sendBeacon('/api/log', JSON.stringify({ event: 'unload' }));
});

// Online/Offline events
window.addEventListener('online', () => {
  console.log('Back online');
});

window.addEventListener('offline', () => {
  console.log('Lost connection');
});

// Storage event - Fires when localStorage changes in another tab
window.addEventListener('storage', (event) => {
  console.log(`Key: ${event.key}`);
  console.log(`Old value: ${event.oldValue}`);
  console.log(`New value: ${event.newValue}`);
});
```

### Local Storage and Session Storage

```javascript
// localStorage - Persists even after browser closes
window.localStorage.setItem('username', 'john');
const username = window.localStorage.getItem('username');
window.localStorage.removeItem('username');
window.localStorage.clear(); // Clear all

// sessionStorage - Clears when tab closes
window.sessionStorage.setItem('tempData', 'value');
const tempData = window.sessionStorage.getItem('tempData');

// Store objects (must stringify)
const user = { name: 'John', age: 30 };
localStorage.setItem('user', JSON.stringify(user));
const storedUser = JSON.parse(localStorage.getItem('user'));

// Check storage quota
if ('storage' in navigator && 'estimate' in navigator.storage) {
  navigator.storage.estimate().then(estimate => {
    console.log(`Used: ${estimate.usage} bytes`);
    console.log(`Quota: ${estimate.quota} bytes`);
  });
}
```

### Request Animation Frame

```javascript
// Optimized animation loop
function animate() {
  // Animation code here
  console.log('Frame rendered');
  
  // Request next frame
  requestAnimationFrame(animate);
}

// Start animation
const animationId = requestAnimationFrame(animate);

// Cancel animation
cancelAnimationFrame(animationId);

// Example: Smooth counter
let count = 0;
let start = null;

function animateCounter(timestamp) {
  if (!start) start = timestamp;
  const progress = timestamp - start;
  
  count = Math.min(Math.floor(progress / 10), 100);
  document.getElementById('counter').textContent = count;
  
  if (count < 100) {
    requestAnimationFrame(animateCounter);
  }
}

requestAnimationFrame(animateCounter);
```

### Practical Examples

#### 1. Responsive Design Helper

```javascript
class WindowHelper {
  static getViewport() {
    return {
      width: window.innerWidth,
      height: window.innerHeight,
      isMobile: window.innerWidth < 768,
      isTablet: window.innerWidth >= 768 && window.innerWidth < 1024,
      isDesktop: window.innerWidth >= 1024
    };
  }

  static onResize(callback, delay = 300) {
    let timeoutId;
    window.addEventListener('resize', () => {
      clearTimeout(timeoutId);
      timeoutId = setTimeout(() => {
        callback(this.getViewport());
      }, delay);
    });
  }
}

// Usage
WindowHelper.onResize((viewport) => {
  console.log('Viewport changed:', viewport);
});
```

#### 2. Scroll Progress Indicator

```javascript
function updateScrollProgress() {
  const windowHeight = window.innerHeight;
  const documentHeight = document.documentElement.scrollHeight;
  const scrollTop = window.scrollY;
  
  const scrollPercentage = (scrollTop / (documentHeight - windowHeight)) * 100;
  
  document.getElementById('progress-bar').style.width = `${scrollPercentage}%`;
}

window.addEventListener('scroll', updateScrollProgress);
```

#### 3. Auto-save with localStorage

```javascript
class AutoSave {
  constructor(key, interval = 5000) {
    this.key = key;
    this.interval = interval;
    this.load();
    this.startAutoSave();
  }

  save(data) {
    localStorage.setItem(this.key, JSON.stringify(data));
  }

  load() {
    const data = localStorage.getItem(this.key);
    return data ? JSON.parse(data) : null;
  }

  startAutoSave() {
    this.intervalId = setInterval(() => {
      const data = this.getData(); // Your method to get current data
      this.save(data);
      console.log('Auto-saved');
    }, this.interval);
  }

  stopAutoSave() {
    clearInterval(this.intervalId);
  }
}
```

### Significance of Window Object

1. **Global Scope** - All global variables/functions are window properties
2. **Browser API Access** - Gateway to all browser APIs
3. **DOM Access** - Access to document and DOM manipulation
4. **Navigation** - Control browser navigation and history
5. **Communication** - Cross-window/iframe communication
6. **Storage** - Client-side data persistence
7. **Events** - Handle browser-level events
8. **Timers** - Schedule code execution
9. **Screen Information** - Responsive design decisions
10. **Browser Information** - Feature detection and compatibility

---

## 95. Explain the Document object.

### What is the Document Object?

The **Document object** represents the HTML document loaded in the browser. It's the entry point to the DOM (Document Object Model) tree and provides methods and properties to access and manipulate HTML elements.

```javascript
// Document is a property of window
console.log(window.document === document); // true

// Document type
console.log(document.constructor.name); // "HTMLDocument"
```

### Document Properties

#### 1. Basic Document Information

```javascript
// Document properties
document.title;              // Page title
document.URL;                // Full URL
document.domain;             // Domain name
document.referrer;           // Referring URL
document.lastModified;       // Last modification date
document.readyState;         // "loading", "interactive", or "complete"
document.characterSet;       // Character encoding (e.g., "UTF-8")

// Example: Change page title
document.title = 'New Page Title';

// Example: Check if document is ready
console.log(document.readyState); // "complete" when fully loaded
```

#### 2. Document Structure References

```javascript
// Root elements
document.documentElement;    // <html> element
document.head;               // <head> element
document.body;               // <body> element

// Special elements
document.forms;              // All <form> elements
document.images;             // All <img> elements
document.links;              // All <a> and <area> elements with href
document.scripts;            // All <script> elements
document.styleSheets;        // All stylesheets

// Example: Access all forms
Array.from(document.forms).forEach(form => {
  console.log(form.id);
});
```

#### 3. Active Elements

```javascript
// Currently focused element
document.activeElement;

// Currently selected text
document.getSelection();

// Example: Get selected text
const selection = document.getSelection();
console.log(selection.toString());

// Example: Check what's focused
document.addEventListener('focusin', () => {
  console.log('Focused:', document.activeElement.tagName);
});
```

### Document Methods - Element Selection

#### 1. getElementById

```javascript
// Get element by ID (returns single element or null)
const element = document.getElementById('myId');

if (element) {
  console.log(element.textContent);
}

// Note: No need for '#' prefix
// ❌ document.getElementById('#myId')
// ✅ document.getElementById('myId')
```

#### 2. getElementsByClassName

```javascript
// Get elements by class (returns HTMLCollection - live)
const elements = document.getElementsByClassName('myClass');

// HTMLCollection is array-like, not an array
console.log(elements.length);
console.log(elements[0]);

// Convert to array for array methods
const elementsArray = Array.from(elements);
elementsArray.forEach(el => {
  console.log(el.textContent);
});

// Multiple classes
const multiClass = document.getElementsByClassName('class1 class2');
```

#### 3. getElementsByTagName

```javascript
// Get elements by tag name (returns HTMLCollection - live)
const divs = document.getElementsByTagName('div');
const allElements = document.getElementsByTagName('*'); // All elements

// Example: Style all paragraphs
Array.from(document.getElementsByTagName('p')).forEach(p => {
  p.style.color = 'blue';
});
```

#### 4. querySelector (Modern - Recommended)

```javascript
// Get first matching element (returns Element or null)
const element = document.querySelector('.myClass');
const firstDiv = document.querySelector('div');
const complexSelector = document.querySelector('div.container > p:first-child');

// CSS selector syntax
document.querySelector('#myId');           // By ID
document.querySelector('.myClass');        // By class
document.querySelector('[data-id="123"]'); // By attribute
document.querySelector('div p');           // Descendant
document.querySelector('div > p');         // Direct child
document.querySelector('p:nth-child(2)');  // Pseudo-selector

// Returns null if not found
const notFound = document.querySelector('.nonexistent');
console.log(notFound); // null
```

#### 5. querySelectorAll (Modern - Recommended)

```javascript
// Get all matching elements (returns NodeList - static)
const elements = document.querySelectorAll('.myClass');

// NodeList can use forEach directly
elements.forEach(element => {
  console.log(element.textContent);
});

// Convert to array (optional)
const elementsArray = [...elements];

// Complex selectors
document.querySelectorAll('div.container p'); // All p in div.container
document.querySelectorAll('[data-active="true"]'); // By data attribute
document.querySelectorAll('li:nth-child(odd)'); // Odd list items
```

#### Comparison: Live vs Static Collections

```javascript
// HTMLCollection (live) - updates automatically
const liveCollection = document.getElementsByClassName('item');
console.log(liveCollection.length); // 3

// Add new element
const newItem = document.createElement('div');
newItem.className = 'item';
document.body.appendChild(newItem);

console.log(liveCollection.length); // 4 (updated automatically!)

// NodeList (static) - doesn't update
const staticList = document.querySelectorAll('.item');
console.log(staticList.length); // 4

// Add another element
const anotherItem = document.createElement('div');
anotherItem.className = 'item';
document.body.appendChild(anotherItem);

console.log(staticList.length); // 4 (not updated)
```

### Document Methods - Element Creation and Manipulation

#### 1. Creating Elements

```javascript
// Create element
const div = document.createElement('div');
const span = document.createElement('span');

// Create text node
const textNode = document.createTextNode('Hello World');

// Create document fragment (performance optimization)
const fragment = document.createDocumentFragment();

// Example: Create complex element
const card = document.createElement('div');
card.className = 'card';
card.innerHTML = `
  <h3>Card Title</h3>
  <p>Card content</p>
`;
document.body.appendChild(card);
```

#### 2. Adding Elements

```javascript
// appendChild - Add as last child
const parent = document.getElementById('parent');
const child = document.createElement('p');
parent.appendChild(child);

// append - Can append multiple nodes and strings
parent.append('Text', child, 'More text');

// prepend - Add as first child
parent.prepend(child);

// insertBefore - Insert before specific element
const reference = document.getElementById('reference');
parent.insertBefore(child, reference);

// after/before - Insert as sibling
reference.after(child);
reference.before(child);
```

#### 3. Removing Elements

```javascript
// Remove element (modern)
const element = document.getElementById('myElement');
element.remove();

// Remove child (traditional)
const parent = document.getElementById('parent');
const child = document.getElementById('child');
parent.removeChild(child);

// Remove all children
while (parent.firstChild) {
  parent.removeChild(parent.firstChild);
}

// Or modern way
parent.replaceChildren();
```

#### 4. Replacing Elements

```javascript
// Replace element
const oldElement = document.getElementById('old');
const newElement = document.createElement('div');
newElement.textContent = 'New content';
oldElement.replaceWith(newElement);

// Replace child
parent.replaceChild(newElement, oldElement);
```

#### 5. Cloning Elements

```javascript
// Clone element
const original = document.getElementById('original');
const clone = original.cloneNode(true); // true = deep clone (includes children)
const shallowClone = original.cloneNode(false); // false = shallow clone

// Cloned element needs to be inserted
document.body.appendChild(clone);

// Event listeners are NOT cloned
```

### Document Write and Content

```javascript
// document.write (avoid in modern code!)
document.write('<h1>Hello</h1>'); // Overwrites entire document if called after load

// Better alternatives:
// 1. innerHTML
document.body.innerHTML = '<h1>Hello</h1>';

// 2. createElement and appendChild
const heading = document.createElement('h1');
heading.textContent = 'Hello';
document.body.appendChild(heading);

// 3. insertAdjacentHTML
element.insertAdjacentHTML('beforeend', '<p>New paragraph</p>');
// Positions: 'beforebegin', 'afterbegin', 'beforeend', 'afterend'
```

### Document Events

```javascript
// DOMContentLoaded - DOM is ready (before images/styles load)
document.addEventListener('DOMContentLoaded', () => {
  console.log('DOM ready!');
  // Safe to manipulate DOM here
});

// readystatechange - Document loading state changes
document.addEventListener('readystatechange', () => {
  console.log('State:', document.readyState);
  // "loading", "interactive", "complete"
});

// selectionchange - Text selection changes
document.addEventListener('selectionchange', () => {
  const selection = document.getSelection();
  console.log('Selected:', selection.toString());
});

// visibilitychange - Page visibility changes (tab switch)
document.addEventListener('visibilitychange', () => {
  if (document.hidden) {
    console.log('Page hidden');
    // Pause video, stop timers, etc.
  } else {
    console.log('Page visible');
    // Resume activity
  }
});
```

### Document Cookies

```javascript
// Get all cookies
console.log(document.cookie);

// Set cookie
document.cookie = 'username=john';
document.cookie = 'theme=dark; max-age=3600'; // Expires in 1 hour
document.cookie = 'session=abc123; path=/; secure; samesite=strict';

// Cookie helper functions
const CookieManager = {
  set(name, value, days) {
    const date = new Date();
    date.setTime(date.getTime() + (days * 24 * 60 * 60 * 1000));
    const expires = `expires=${date.toUTCString()}`;
    document.cookie = `${name}=${value};${expires};path=/`;
  },

  get(name) {
    const cookies = document.cookie.split(';');
    for (let cookie of cookies) {
      const [key, value] = cookie.trim().split('=');
      if (key === name) return value;
    }
    return null;
  },

  delete(name) {
    document.cookie = `${name}=;expires=Thu, 01 Jan 1970 00:00:00 UTC;path=/`;
  }
};

// Usage
CookieManager.set('user', 'john', 7); // Set for 7 days
console.log(CookieManager.get('user')); // "john"
CookieManager.delete('user');
```

### Practical Examples

#### 1. Dynamic Content Loader

```javascript
class ContentLoader {
  static loadContent(containerId, content) {
    const container = document.getElementById(containerId);
    
    if (!container) {
      console.error('Container not found');
      return;
    }

    // Clear existing content
    container.innerHTML = '';

    // Create fragment for performance
    const fragment = document.createDocumentFragment();

    content.forEach(item => {
      const element = document.createElement('div');
      element.className = 'content-item';
      element.innerHTML = `
        <h3>${item.title}</h3>
        <p>${item.description}</p>
      `;
      fragment.appendChild(element);
    });

    container.appendChild(fragment);
  }
}

// Usage
const data = [
  { title: 'Item 1', description: 'Description 1' },
  { title: 'Item 2', description: 'Description 2' }
];
ContentLoader.loadContent('container', data);
```

#### 2. Element Factory

```javascript
class ElementFactory {
  static create(tag, options = {}) {
    const element = document.createElement(tag);

    // Set attributes
    if (options.id) element.id = options.id;
    if (options.className) element.className = options.className;
    if (options.text) element.textContent = options.text;
    if (options.html) element.innerHTML = options.html;

    // Set data attributes
    if (options.data) {
      Object.entries(options.data).forEach(([key, value]) => {
        element.dataset[key] = value;
      });
    }

    // Set styles
    if (options.styles) {
      Object.assign(element.style, options.styles);
    }

    // Add event listeners
    if (options.events) {
      Object.entries(options.events).forEach(([event, handler]) => {
        element.addEventListener(event, handler);
      });
    }

    return element;
  }
}

// Usage
const button = ElementFactory.create('button', {
  id: 'myButton',
  className: 'btn btn-primary',
  text: 'Click Me',
  data: { userId: '123' },
  styles: { padding: '10px', backgroundColor: 'blue' },
  events: {
    click: () => alert('Clicked!')
  }
});

document.body.appendChild(button);
```

#### 3. DOM Observer

```javascript
// Watch for document ready
function onDocumentReady(callback) {
  if (document.readyState === 'loading') {
    document.addEventListener('DOMContentLoaded', callback);
  } else {
    callback();
  }
}

// Usage
onDocumentReady(() => {
  console.log('Document is ready!');
  // Initialize your app
});
```

### Document vs Window

| Feature | Document | Window |
|---------|----------|--------|
| Represents | HTML document | Browser window |
| Parent | window.document | Global object |
| DOM Access | Yes | No (through document) |
| Events | DOM events | Browser events |
| Methods | DOM manipulation | Browser control |
| Scope | Document tree | Entire browser |

---

## 96. What new features does HTML5 bring to JavaScript development?

### Overview

HTML5 introduced numerous APIs and features that significantly enhanced JavaScript's capabilities for web development, enabling richer, more interactive applications.

### 1. Canvas API

**2D Graphics Drawing**

```javascript
// Get canvas context
const canvas = document.getElementById('myCanvas');
const ctx = canvas.getContext('2d');

// Draw shapes
ctx.fillStyle = 'blue';
ctx.fillRect(10, 10, 100, 100); // Rectangle

ctx.strokeStyle = 'red';
ctx.lineWidth = 5;
ctx.strokeRect(150, 10, 100, 100); // Outlined rectangle

// Draw circle
ctx.beginPath();
ctx.arc(75, 200, 50, 0, Math.PI * 2);
ctx.fillStyle = 'green';
ctx.fill();

// Draw text
ctx.font = '30px Arial';
ctx.fillStyle = 'black';
ctx.fillText('Hello Canvas!', 10, 300);

// Draw image
const img = new Image();
img.onload = () => {
  ctx.drawImage(img, 0, 0);
};
img.src = 'image.jpg';

// Clear canvas
ctx.clearRect(0, 0, canvas.width, canvas.height);
```

**Animation Example:**

```javascript
class CanvasAnimation {
  constructor(canvasId) {
    this.canvas = document.getElementById(canvasId);
    this.ctx = this.canvas.getContext('2d');
    this.x = 0;
    this.animate = this.animate.bind(this);
  }

  animate() {
    // Clear canvas
    this.ctx.clearRect(0, 0, this.canvas.width, this.canvas.height);

    // Draw moving circle
    this.ctx.beginPath();
    this.ctx.arc(this.x, 100, 20, 0, Math.PI * 2);
    this.ctx.fillStyle = 'blue';
    this.ctx.fill();

    // Update position
    this.x = (this.x + 2) % this.canvas.width;

    // Request next frame
    requestAnimationFrame(this.animate);
  }

  start() {
    this.animate();
  }
}

const animation = new CanvasAnimation('myCanvas');
animation.start();
```

### 2. Web Storage API

**localStorage - Persistent Storage**

```javascript
// Store data (persists after browser closes)
localStorage.setItem('username', 'john');
localStorage.setItem('theme', 'dark');

// Retrieve data
const username = localStorage.getItem('username');

// Remove item
localStorage.removeItem('username');

// Clear all
localStorage.clear();

// Get number of items
console.log(localStorage.length);

// Iterate through all items
for (let i = 0; i < localStorage.length; i++) {
  const key = localStorage.key(i);
  console.log(`${key}: ${localStorage.getItem(key)}`);
}

// Store objects (must stringify)
const user = { name: 'John', age: 30, email: 'john@example.com' };
localStorage.setItem('user', JSON.stringify(user));

// Retrieve and parse objects
const storedUser = JSON.parse(localStorage.getItem('user'));
console.log(storedUser.name); // "John"
```

**sessionStorage - Temporary Storage**

```javascript
// Store data (clears when tab closes)
sessionStorage.setItem('cartItems', JSON.stringify(items));

// Retrieve data
const cartItems = JSON.parse(sessionStorage.getItem('cartItems'));

// Same API as localStorage
sessionStorage.removeItem('cartItems');
sessionStorage.clear();
```

**Storage Helper Class:**

```javascript
class StorageManager {
  static set(key, value, type = 'local') {
    const storage = type === 'local' ? localStorage : sessionStorage;
    const data = typeof value === 'object' ? JSON.stringify(value) : value;
    storage.setItem(key, data);
  }

  static get(key, type = 'local') {
    const storage = type === 'local' ? localStorage : sessionStorage;
    const data = storage.getItem(key);
    
    try {
      return JSON.parse(data);
    } catch {
      return data;
    }
  }

  static remove(key, type = 'local') {
    const storage = type === 'local' ? localStorage : sessionStorage;
    storage.removeItem(key);
  }

  static clear(type = 'local') {
    const storage = type === 'local' ? localStorage : sessionStorage;
    storage.clear();
  }
}

// Usage
StorageManager.set('user', { name: 'John' });
const user = StorageManager.get('user');
```

### 3. Geolocation API

```javascript
// Check if geolocation is available
if ('geolocation' in navigator) {
  // Get current position (one-time)
  navigator.geolocation.getCurrentPosition(
    (position) => {
      console.log('Latitude:', position.coords.latitude);
      console.log('Longitude:', position.coords.longitude);
      console.log('Accuracy:', position.coords.accuracy, 'meters');
      console.log('Altitude:', position.coords.altitude);
      console.log('Speed:', position.coords.speed);
    },
    (error) => {
      switch(error.code) {
        case error.PERMISSION_DENIED:
          console.error('User denied geolocation');
          break;
        case error.POSITION_UNAVAILABLE:
          console.error('Location unavailable');
          break;
        case error.TIMEOUT:
          console.error('Request timeout');
          break;
      }
    },
    {
      enableHighAccuracy: true,  // Use GPS if available
      timeout: 5000,             // Wait max 5 seconds
      maximumAge: 0              // Don't use cached position
    }
  );

  // Watch position (continuous updates)
  const watchId = navigator.geolocation.watchPosition(
    (position) => {
      updateMap(position.coords.latitude, position.coords.longitude);
    },
    (error) => console.error(error),
    { enableHighAccuracy: true }
  );

  // Stop watching
  navigator.geolocation.clearWatch(watchId);
}

// Calculate distance between two points
function calculateDistance(lat1, lon1, lat2, lon2) {
  const R = 6371; // Earth radius in km
  const dLat = (lat2 - lat1) * Math.PI / 180;
  const dLon = (lon2 - lon1) * Math.PI / 180;
  const a = Math.sin(dLat/2) * Math.sin(dLat/2) +
            Math.cos(lat1 * Math.PI / 180) * Math.cos(lat2 * Math.PI / 180) *
            Math.sin(dLon/2) * Math.sin(dLon/2);
  const c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1-a));
  return R * c; // Distance in km
}
```

### 4. Web Workers

**Background Threading for Heavy Computations**

**Main Script:**
```javascript
// Create worker
const worker = new Worker('worker.js');

// Send message to worker
worker.postMessage({ type: 'start', data: [1, 2, 3, 4, 5] });

// Receive message from worker
worker.addEventListener('message', (event) => {
  console.log('Result from worker:', event.data);
});

// Handle errors
worker.addEventListener('error', (error) => {
  console.error('Worker error:', error.message);
});

// Terminate worker
worker.terminate();
```

**worker.js:**
```javascript
// Listen for messages
self.addEventListener('message', (event) => {
  const { type, data } = event.data;

  if (type === 'start') {
    // Perform heavy computation
    const result = performHeavyCalculation(data);
    
    // Send result back to main thread
    self.postMessage(result);
  }
});

function performHeavyCalculation(data) {
  // Simulate heavy work
  let sum = 0;
  for (let i = 0; i < 1000000000; i++) {
    sum += Math.sqrt(i);
  }
  return sum;
}

// Example: Process large dataset
self.addEventListener('message', (event) => {
  const largeArray = event.data;
  
  // Process without blocking main thread
  const processed = largeArray.map(item => item * 2);
  
  self.postMessage(processed);
});
```

### 5. Drag and Drop API

```javascript
// HTML
// <div id="draggable" draggable="true">Drag me</div>
// <div id="dropzone">Drop here</div>

// Make element draggable
const draggable = document.getElementById('draggable');
const dropzone = document.getElementById('dropzone');

// Drag start
draggable.addEventListener('dragstart', (e) => {
  e.dataTransfer.effectAllowed = 'move';
  e.dataTransfer.setData('text/html', e.target.innerHTML);
  e.target.style.opacity = '0.5';
});

// Drag end
draggable.addEventListener('dragend', (e) => {
  e.target.style.opacity = '1';
});

// Drop zone events
dropzone.addEventListener('dragover', (e) => {
  e.preventDefault(); // Allow drop
  e.dataTransfer.dropEffect = 'move';
  dropzone.classList.add('drag-over');
});

dropzone.addEventListener('dragleave', (e) => {
  dropzone.classList.remove('drag-over');
});

dropzone.addEventListener('drop', (e) => {
  e.preventDefault();
  const data = e.dataTransfer.getData('text/html');
  dropzone.innerHTML = data;
  dropzone.classList.remove('drag-over');
});

// File drag and drop
const fileDropzone = document.getElementById('file-dropzone');

fileDropzone.addEventListener('drop', (e) => {
  e.preventDefault();
  
  const files = e.dataTransfer.files;
  
  Array.from(files).forEach(file => {
    console.log('File:', file.name);
    console.log('Type:', file.type);
    console.log('Size:', file.size, 'bytes');
    
    // Read file
    const reader = new FileReader();
    reader.onload = (event) => {
      console.log('File content:', event.target.result);
    };
    reader.readAsText(file);
  });
});
```

### 6. History API

**Manipulate Browser History Without Page Reload**

```javascript
// Push new state (adds to history)
const state = { page: 1, data: 'some data' };
const title = 'Page 1';
const url = '/page1';
history.pushState(state, title, url);

// Replace current state (doesn't add to history)
history.replaceState({ page: 2 }, 'Page 2', '/page2');

// Navigate
history.back();     // Go back
history.forward();  // Go forward
history.go(-2);     // Go back 2 pages
history.go(1);      // Go forward 1 page

// Listen to state changes
window.addEventListener('popstate', (event) => {
  console.log('State:', event.state);
  console.log('Location:', location.pathname);
  
  // Update page content based on state
  if (event.state) {
    updatePageContent(event.state);
  }
});

// Single Page Application (SPA) example
class Router {
  constructor(routes) {
    this.routes = routes;
    this.init();
  }

  init() {
    // Handle popstate (back/forward buttons)
    window.addEventListener('popstate', () => {
      this.handleRoute(location.pathname);
    });

    // Handle link clicks
    document.addEventListener('click', (e) => {
      if (e.target.matches('[data-link]')) {
        e.preventDefault();
        this.navigate(e.target.href);
      }
    });

    // Initial route
    this.handleRoute(location.pathname);
  }

  navigate(url) {
    history.pushState(null, null, url);
    this.handleRoute(url);
  }

  handleRoute(path) {
    const route = this.routes[path] || this.routes['/404'];
    document.getElementById('app').innerHTML = route();
  }
}

// Usage
const router = new Router({
  '/': () => '<h1>Home Page</h1>',
  '/about': () => '<h1>About Page</h1>',
  '/404': () => '<h1>404 - Not Found</h1>'
});
```

### 7. Audio and Video API

```javascript
// Get video element
const video = document.getElementById('myVideo');

// Control playback
video.play();
video.pause();
video.load();     // Reload video

// Properties
video.currentTime = 10;        // Seek to 10 seconds
video.playbackRate = 1.5;      // 1.5x speed
video.volume = 0.5;            // 50% volume
video.muted = true;            // Mute

// Read-only properties
console.log(video.duration);   // Total duration
console.log(video.paused);     // Is paused?
console.log(video.ended);      // Has ended?
console.log(video.buffered);   // Buffered ranges

// Events
video.addEventListener('play', () => {
  console.log('Video started playing');
});

video.addEventListener('pause', () => {
  console.log('Video paused');
});

video.addEventListener('ended', () => {
  console.log('Video ended');
});

video.addEventListener('timeupdate', () => {
  const progress = (video.currentTime / video.duration) * 100;
  console.log(`Progress: ${progress}%`);
});

video.addEventListener('loadedmetadata', () => {
  console.log(`Duration: ${video.duration} seconds`);
});

// Custom video player
class VideoPlayer {
  constructor(videoId) {
    this.video = document.getElementById(videoId);
    this.setupControls();
  }

  setupControls() {
    // Play/Pause button
    document.getElementById('playBtn').addEventListener('click', () => {
      if (this.video.paused) {
        this.video.play();
      } else {
        this.video.pause();
      }
    });

    // Progress bar
    document.getElementById('progress').addEventListener('click', (e) => {
      const rect = e.target.getBoundingClientRect();
      const percent = (e.clientX - rect.left) / rect.width;
      this.video.currentTime = percent * this.video.duration;
    });

    // Volume control
    document.getElementById('volume').addEventListener('input', (e) => {
      this.video.volume = e.target.value;
    });

    // Fullscreen
    document.getElementById('fullscreen').addEventListener('click', () => {
      if (this.video.requestFullscreen) {
        this.video.requestFullscreen();
      }
    });
  }
}

// Audio API (same as video)
const audio = new Audio('song.mp3');
audio.play();
```

### 8. Form Enhancements

```javascript
// New input types with validation
// <input type="email" required>
// <input type="url" required>
// <input type="number" min="0" max="100">
// <input type="date">
// <input type="time">
// <input type="color">
// <input type="range" min="0" max="100">

// Form validation
const form = document.getElementById('myForm');

form.addEventListener('submit', (e) => {
  e.preventDefault();

  // Check validity
  if (!form.checkValidity()) {
    console.log('Form is invalid');
    
    // Show validation messages
    Array.from(form.elements).forEach(element => {
      if (!element.checkValidity()) {
        console.log(`${element.name}: ${element.validationMessage}`);
      }
    });
    return;
  }

  // Form is valid
  const formData = new FormData(form);
  console.log(Object.fromEntries(formData));
});

// Custom validation
const email = document.getElementById('email');

email.addEventListener('input', () => {
  if (email.value.includes('test')) {
    email.setCustomValidity('Test emails are not allowed');
  } else {
    email.setCustomValidity(''); // Clear error
  }
});

// Pattern validation
const input = document.getElementById('username');
input.pattern = '[A-Za-z]{3,}'; // At least 3 letters

// Required validation
input.required = true;

// Validation states
console.log(input.validity.valid);        // Overall validity
console.log(input.validity.valueMissing); // Required but empty
console.log(input.validity.typeMismatch); // Wrong type
console.log(input.validity.patternMismatch); // Pattern doesn't match
console.log(input.validity.tooLong);      // Too long
console.log(input.validity.tooShort);     // Too short
console.log(input.validity.rangeUnderflow); // Below min
console.log(input.validity.rangeOverflow);  // Above max
```

### 9. WebSocket API

**Real-time Bidirectional Communication**

```javascript
// Create WebSocket connection
const socket = new WebSocket('ws://localhost:8080');

// Connection opened
socket.addEventListener('open', (event) => {
  console.log('Connected to server');
  socket.send('Hello Server!');
});

// Listen for messages
socket.addEventListener('message', (event) => {
  console.log('Message from server:', event.data);
  
  // Parse JSON if needed
  try {
    const data = JSON.parse(event.data);
    handleServerMessage(data);
  } catch (e) {
    console.log('Plain text message:', event.data);
  }
});

// Handle errors
socket.addEventListener('error', (error) => {
  console.error('WebSocket error:', error);
});

// Connection closed
socket.addEventListener('close', (event) => {
  console.log('Disconnected from server');
  console.log('Code:', event.code);
  console.log('Reason:', event.reason);
});

// Send messages
function sendMessage(message) {
  if (socket.readyState === WebSocket.OPEN) {
    socket.send(JSON.stringify(message));
  } else {
    console.error('WebSocket is not open');
  }
}

// Close connection
socket.close(1000, 'Normal closure');

// WebSocket states
console.log(socket.readyState);
// 0 = CONNECTING
// 1 = OPEN
// 2 = CLOSING
// 3 = CLOSED

// Chat application example
class ChatClient {
  constructor(url) {
    this.socket = new WebSocket(url);
    this.setupEventListeners();
  }

  setupEventListeners() {
    this.socket.addEventListener('open', () => {
      console.log('Chat connected');
    });

    this.socket.addEventListener('message', (event) => {
      const message = JSON.parse(event.data);
      this.displayMessage(message);
    });

    this.socket.addEventListener('close', () => {
      console.log('Chat disconnected');
      this.reconnect();
    });
  }

  sendMessage(text) {
    const message = {
      type: 'chat',
      text: text,
      timestamp: Date.now()
    };
    this.socket.send(JSON.stringify(message));
  }

  displayMessage(message) {
    const messageElement = document.createElement('div');
    messageElement.textContent = `${message.user}: ${message.text}`;
    document.getElementById('messages').appendChild(messageElement);
  }

  reconnect() {
    setTimeout(() => {
      console.log('Reconnecting...');
      this.socket = new WebSocket(this.url);
      this.setupEventListeners();
    }, 3000);
  }
}
```

### 10. Offline/Online Detection

```javascript
// Check online status
if (navigator.onLine) {
  console.log('Online');
} else {
  console.log('Offline');
}

// Listen for connection changes
window.addEventListener('online', () => {
  console.log('Connection restored');
  syncData(); // Sync offline data
});

window.addEventListener('offline', () => {
  console.log('Connection lost');
  showOfflineMessage();
});

// Offline-first application example
class OfflineManager {
  constructor() {
    this.queue = [];
    this.setupListeners();
  }

  setupListeners() {
    window.addEventListener('online', () => {
      this.processQueue();
    });
  }

  async makeRequest(url, options) {
    if (navigator.onLine) {
      return fetch(url, options);
    } else {
      // Queue request for later
      this.queue.push({ url, options });
      console.log('Request queued for when online');
      return Promise.reject(new Error('Offline'));
    }
  }

  async processQueue() {
    console.log(`Processing ${this.queue.length} queued requests`);
    
    while (this.queue.length > 0) {
      const { url, options } = this.queue.shift();
      try {
        await fetch(url, options);
        console.log('Queued request sent:', url);
      } catch (error) {
        console.error('Failed to send queued request:', error);
        this.queue.unshift({ url, options }); // Re-queue
        break;
      }
    }
  }
}
```

### 11. Semantic Elements & Accessibility

```javascript
// New semantic elements improve accessibility
// <article>, <section>, <nav>, <header>, <footer>, <aside>, <main>

// ARIA attributes for accessibility
const button = document.createElement('button');
button.setAttribute('aria-label', 'Close dialog');
button.setAttribute('aria-expanded', 'false');

// Custom element example
class CustomButton extends HTMLElement {
  constructor() {
    super();
    this.attachShadow({ mode: 'open' });
  }

  connectedCallback() {
    this.shadowRoot.innerHTML = `
      <button>
        <slot></slot>
      </button>
    `;
  }
}

customElements.define('custom-button', CustomButton);

// Usage: <custom-button>Click me</custom-button>
```

### 12. Other Notable APIs

```javascript
// Page Visibility API
document.addEventListener('visibilitychange', () => {
  if (document.hidden) {
    pauseVideo();
  } else {
    resumeVideo();
  }
});

// Fullscreen API
element.requestFullscreen();
document.exitFullscreen();
console.log(document.fullscreenElement);

// Clipboard API
navigator.clipboard.writeText('Copied text').then(() => {
  console.log('Text copied');
});

navigator.clipboard.readText().then(text => {
  console.log('Clipboard content:', text);
});

// Battery Status API (deprecated but useful to know)
navigator.getBattery().then(battery => {
  console.log('Battery level:', battery.level * 100 + '%');
  console.log('Charging:', battery.charging);
});

// Vibration API (mobile)
navigator.vibrate(200); // Vibrate for 200ms
navigator.vibrate([100, 50, 100]); // Pattern

// Screen Orientation API
screen.orientation.lock('landscape');
screen.orientation.unlock();
console.log(screen.orientation.type); // 'portrait-primary', etc.
```

### Summary of HTML5 Benefits

1. **Rich Graphics** - Canvas and SVG for visualizations
2. **Multimedia** - Native audio/video without plugins
3. **Storage** - Client-side data persistence
4. **Real-time Communication** - WebSockets for instant updates
5. **Background Processing** - Web Workers for performance
6. **User Experience** - Drag & drop, geolocation
7. **Form Validation** - Built-in validation
8. **Offline Support** - Service workers and offline detection
9. **Semantic HTML** - Better structure and accessibility
10. **Modern APIs** - History, notifications, and more

HTML5 transformed JavaScript from a simple scripting language into a platform for building sophisticated, feature-rich web applications.



## 97. Discuss the role of JavaScript in Progressive Web Apps (PWAs).

### What are Progressive Web Apps (PWAs)?

**Progressive Web Apps** are web applications that use modern web technologies to deliver app-like experiences. They combine the best of web and native apps, providing:

- **Reliable** - Work offline or on poor networks
- **Fast** - Respond quickly to user interactions
- **Engaging** - Feel like native apps with immersive experiences

JavaScript is the **core technology** that powers PWAs, enabling features like offline functionality, push notifications, and native-like interactions.

### Core PWA Technologies (JavaScript-Powered)

```
┌─────────────────────────────────────┐
│      Progressive Web App            │
├─────────────────────────────────────┤
│  Service Workers (JavaScript)       │
│  Web App Manifest (JSON)            │
│  HTTPS                              │
│  Responsive Design                  │
│  Push Notifications (JavaScript)    │
│  Cache API (JavaScript)             │
└─────────────────────────────────────┘
```

### 1. Service Workers

**Service Workers** are the backbone of PWAs - JavaScript files that run in the background, separate from the web page.

#### Basic Service Worker Registration

```javascript
// In your main JavaScript file (app.js)

// Check if service workers are supported
if ('serviceWorker' in navigator) {
  window.addEventListener('load', () => {
    navigator.serviceWorker.register('/service-worker.js')
      .then(registration => {
        console.log('Service Worker registered:', registration.scope);
        
        // Check for updates
        registration.update();
      })
      .catch(error => {
        console.error('Service Worker registration failed:', error);
      });
  });

  // Listen for updates
  navigator.serviceWorker.addEventListener('controllerchange', () => {
    console.log('New Service Worker activated');
    // Optionally reload the page
    window.location.reload();
  });
}
```

#### Service Worker Lifecycle

```javascript
// service-worker.js

const CACHE_NAME = 'my-pwa-cache-v1';
const urlsToCache = [
  '/',
  '/index.html',
  '/styles/main.css',
  '/scripts/app.js',
  '/images/logo.png'
];

// Install event - cache assets
self.addEventListener('install', (event) => {
  console.log('Service Worker installing...');
  
  event.waitUntil(
    caches.open(CACHE_NAME)
      .then(cache => {
        console.log('Cache opened');
        return cache.addAll(urlsToCache);
      })
      .then(() => {
        // Force the waiting service worker to become active
        return self.skipWaiting();
      })
  );
});

// Activate event - clean up old caches
self.addEventListener('activate', (event) => {
  console.log('Service Worker activating...');
  
  event.waitUntil(
    caches.keys().then(cacheNames => {
      return Promise.all(
        cacheNames.map(cacheName => {
          if (cacheName !== CACHE_NAME) {
            console.log('Deleting old cache:', cacheName);
            return caches.delete(cacheName);
          }
        })
      );
    }).then(() => {
      // Take control of all pages immediately
      return self.clients.claim();
    })
  );
});

// Fetch event - serve from cache or network
self.addEventListener('fetch', (event) => {
  event.respondWith(
    caches.match(event.request)
      .then(response => {
        // Return cached version or fetch from network
        return response || fetch(event.request);
      })
      .catch(() => {
        // Return offline page if available
        return caches.match('/offline.html');
      })
  );
});
```

### 2. Caching Strategies

#### Cache First (Good for static assets)

```javascript
// service-worker.js

self.addEventListener('fetch', (event) => {
  event.respondWith(
    caches.match(event.request)
      .then(cachedResponse => {
        if (cachedResponse) {
          return cachedResponse; // Return from cache
        }
        
        // Not in cache, fetch from network
        return fetch(event.request).then(response => {
          // Cache the new response
          return caches.open(CACHE_NAME).then(cache => {
            cache.put(event.request, response.clone());
            return response;
          });
        });
      })
  );
});
```

#### Network First (Good for dynamic content)

```javascript
self.addEventListener('fetch', (event) => {
  event.respondWith(
    fetch(event.request)
      .then(response => {
        // Update cache with fresh content
        const responseClone = response.clone();
        caches.open(CACHE_NAME).then(cache => {
          cache.put(event.request, responseClone);
        });
        return response;
      })
      .catch(() => {
        // Network failed, try cache
        return caches.match(event.request);
      })
  );
});
```

#### Stale While Revalidate (Good for balance)

```javascript
self.addEventListener('fetch', (event) => {
  event.respondWith(
    caches.match(event.request).then(cachedResponse => {
      const fetchPromise = fetch(event.request).then(networkResponse => {
        caches.open(CACHE_NAME).then(cache => {
          cache.put(event.request, networkResponse.clone());
        });
        return networkResponse;
      });
      
      // Return cached version immediately, update in background
      return cachedResponse || fetchPromise;
    })
  );
});
```

#### Advanced Caching Strategy

```javascript
// service-worker.js

const CACHE_NAME = 'pwa-v1';
const CACHE_URLS = {
  static: [
    '/',
    '/index.html',
    '/styles/main.css',
    '/scripts/app.js',
    '/offline.html'
  ],
  dynamic: 'dynamic-cache-v1'
};

// Install
self.addEventListener('install', (event) => {
  event.waitUntil(
    caches.open(CACHE_NAME)
      .then(cache => cache.addAll(CACHE_URLS.static))
      .then(() => self.skipWaiting())
  );
});

// Activate
self.addEventListener('activate', (event) => {
  event.waitUntil(
    caches.keys().then(keys => {
      return Promise.all(
        keys.filter(key => key !== CACHE_NAME && key !== CACHE_URLS.dynamic)
          .map(key => caches.delete(key))
      );
    }).then(() => self.clients.claim())
  );
});

// Fetch with strategy routing
self.addEventListener('fetch', (event) => {
  const { request } = event;
  const url = new URL(request.url);

  // Strategy 1: Cache first for static assets
  if (CACHE_URLS.static.includes(url.pathname)) {
    event.respondWith(cacheFirst(request));
  }
  // Strategy 2: Network first for API calls
  else if (url.pathname.startsWith('/api/')) {
    event.respondWith(networkFirst(request));
  }
  // Strategy 3: Stale while revalidate for images
  else if (request.destination === 'image') {
    event.respondWith(staleWhileRevalidate(request));
  }
  // Strategy 4: Network only for everything else
  else {
    event.respondWith(fetch(request));
  }
});

// Helper functions
async function cacheFirst(request) {
  const cached = await caches.match(request);
  return cached || fetch(request);
}

async function networkFirst(request) {
  try {
    const response = await fetch(request);
    const cache = await caches.open(CACHE_URLS.dynamic);
    cache.put(request, response.clone());
    return response;
  } catch (error) {
    return caches.match(request);
  }
}

async function staleWhileRevalidate(request) {
  const cached = await caches.match(request);
  
  const fetchPromise = fetch(request).then(response => {
    const cache = caches.open(CACHE_URLS.dynamic);
    cache.then(c => c.put(request, response.clone()));
    return response;
  });

  return cached || fetchPromise;
}
```

### 3. Web App Manifest

**manifest.json** - Defines app metadata (configured via JavaScript)

```json
{
  "name": "My Progressive Web App",
  "short_name": "MyPWA",
  "description": "A full-featured PWA example",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#2196F3",
  "orientation": "portrait",
  "icons": [
    {
      "src": "/icons/icon-72x72.png",
      "sizes": "72x72",
      "type": "image/png"
    },
    {
      "src": "/icons/icon-128x128.png",
      "sizes": "128x128",
      "type": "image/png"
    },
    {
      "src": "/icons/icon-192x192.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "/icons/icon-512x512.png",
      "sizes": "512x512",
      "type": "image/png"
    }
  ],
  "categories": ["productivity", "utilities"],
  "shortcuts": [
    {
      "name": "New Document",
      "short_name": "New",
      "description": "Create a new document",
      "url": "/new",
      "icons": [{ "src": "/icons/new.png", "sizes": "96x96" }]
    }
  ]
}
```

**Link manifest in HTML:**
```html
<link rel="manifest" href="/manifest.json">
```

**Dynamic manifest generation (JavaScript):**
```javascript
// Generate manifest dynamically based on user preferences
function generateManifest(theme) {
  const manifest = {
    name: 'My PWA',
    short_name: 'PWA',
    start_url: '/',
    display: 'standalone',
    theme_color: theme === 'dark' ? '#000000' : '#2196F3',
    background_color: theme === 'dark' ? '#121212' : '#ffffff',
    icons: [
      {
        src: `/icons/icon-${theme}-192.png`,
        sizes: '192x192',
        type: 'image/png'
      }
    ]
  };

  const blob = new Blob([JSON.stringify(manifest)], { type: 'application/json' });
  const manifestURL = URL.createObjectURL(blob);
  
  document.querySelector('link[rel="manifest"]').href = manifestURL;
}
```

### 4. Push Notifications

**Request Permission:**
```javascript
// app.js

async function requestNotificationPermission() {
  if (!('Notification' in window)) {
    console.log('Notifications not supported');
    return false;
  }

  if (Notification.permission === 'granted') {
    return true;
  }

  if (Notification.permission !== 'denied') {
    const permission = await Notification.requestPermission();
    return permission === 'granted';
  }

  return false;
}

// Usage
requestNotificationPermission().then(granted => {
  if (granted) {
    console.log('Notification permission granted');
    subscribeToPushNotifications();
  }
});
```

**Subscribe to Push Notifications:**
```javascript
async function subscribeToPushNotifications() {
  const registration = await navigator.serviceWorker.ready;

  // Check if already subscribed
  let subscription = await registration.pushManager.getSubscription();

  if (!subscription) {
    // Subscribe
    const vapidPublicKey = 'YOUR_PUBLIC_VAPID_KEY';
    const convertedVapidKey = urlBase64ToUint8Array(vapidPublicKey);

    subscription = await registration.pushManager.subscribe({
      userVisibleOnly: true,
      applicationServerKey: convertedVapidKey
    });
  }

  // Send subscription to server
  await fetch('/api/subscribe', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(subscription)
  });

  console.log('Subscribed to push notifications');
}

// Helper function
function urlBase64ToUint8Array(base64String) {
  const padding = '='.repeat((4 - base64String.length % 4) % 4);
  const base64 = (base64String + padding)
    .replace(/\-/g, '+')
    .replace(/_/g, '/');

  const rawData = window.atob(base64);
  const outputArray = new Uint8Array(rawData.length);

  for (let i = 0; i < rawData.length; ++i) {
    outputArray[i] = rawData.charCodeAt(i);
  }
  return outputArray;
}
```

**Handle Push Events in Service Worker:**
```javascript
// service-worker.js

self.addEventListener('push', (event) => {
  console.log('Push notification received');

  let data = { title: 'New Notification', body: 'You have a new message' };

  if (event.data) {
    data = event.data.json();
  }

  const options = {
    body: data.body,
    icon: '/icons/icon-192x192.png',
    badge: '/icons/badge-72x72.png',
    image: data.image,
    vibrate: [200, 100, 200],
    data: {
      url: data.url || '/',
      timestamp: Date.now()
    },
    actions: [
      { action: 'open', title: 'Open', icon: '/icons/open.png' },
      { action: 'close', title: 'Close', icon: '/icons/close.png' }
    ],
    requireInteraction: false,
    tag: 'notification-tag',
    renotify: true
  };

  event.waitUntil(
    self.registration.showNotification(data.title, options)
  );
});

// Handle notification clicks
self.addEventListener('notificationclick', (event) => {
  console.log('Notification clicked:', event.action);

  event.notification.close();

  if (event.action === 'open') {
    event.waitUntil(
      clients.openWindow(event.notification.data.url)
    );
  } else if (event.action === 'close') {
    // Just close the notification
  } else {
    // Default action - open app
    event.waitUntil(
      clients.matchAll({ type: 'window', includeUncontrolled: true })
        .then(clientList => {
          // Focus existing window if open
          for (let client of clientList) {
            if (client.url === '/' && 'focus' in client) {
              return client.focus();
            }
          }
          // Otherwise open new window
          if (clients.openWindow) {
            return clients.openWindow('/');
          }
        })
    );
  }
});

// Handle notification close
self.addEventListener('notificationclose', (event) => {
  console.log('Notification closed');
  // Track analytics
});
```

### 5. Background Sync

**Queue actions for when online:**

```javascript
// app.js - Register sync
async function saveData(data) {
  if ('serviceWorker' in navigator && 'SyncManager' in window) {
    const registration = await navigator.serviceWorker.ready;

    // Save data to IndexedDB
    await saveToIndexedDB(data);

    // Register sync
    try {
      await registration.sync.register('sync-data');
      console.log('Sync registered');
    } catch (error) {
      console.error('Sync registration failed:', error);
      // Fallback: try to send immediately
      await sendDataToServer(data);
    }
  } else {
    // No background sync support
    await sendDataToServer(data);
  }
}

// service-worker.js - Handle sync
self.addEventListener('sync', (event) => {
  if (event.tag === 'sync-data') {
    event.waitUntil(syncData());
  }
});

async function syncData() {
  try {
    const data = await getFromIndexedDB();
    
    for (let item of data) {
      const response = await fetch('/api/sync', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(item)
      });

      if (response.ok) {
        await removeFromIndexedDB(item.id);
      }
    }
    
    console.log('Data synced successfully');
  } catch (error) {
    console.error('Sync failed:', error);
    throw error; // Retry sync later
  }
}
```

### 6. IndexedDB for Offline Storage

```javascript
// db.js - Database management

class PWADatabase {
  constructor(dbName = 'PWA-DB', version = 1) {
    this.dbName = dbName;
    this.version = version;
    this.db = null;
  }

  async init() {
    return new Promise((resolve, reject) => {
      const request = indexedDB.open(this.dbName, this.version);

      request.onerror = () => reject(request.error);
      request.onsuccess = () => {
        this.db = request.result;
        resolve(this.db);
      };

      request.onupgradeneeded = (event) => {
        const db = event.target.result;

        // Create object stores
        if (!db.objectStoreNames.contains('posts')) {
          const postStore = db.createObjectStore('posts', { keyPath: 'id', autoIncrement: true });
          postStore.createIndex('timestamp', 'timestamp', { unique: false });
          postStore.createIndex('synced', 'synced', { unique: false });
        }

        if (!db.objectStoreNames.contains('cache')) {
          db.createObjectStore('cache', { keyPath: 'url' });
        }
      };
    });
  }

  async add(storeName, data) {
    const transaction = this.db.transaction([storeName], 'readwrite');
    const store = transaction.objectStore(storeName);
    return store.add(data);
  }

  async get(storeName, key) {
    const transaction = this.db.transaction([storeName], 'readonly');
    const store = transaction.objectStore(storeName);
    return store.get(key);
  }

  async getAll(storeName) {
    const transaction = this.db.transaction([storeName], 'readonly');
    const store = transaction.objectStore(storeName);
    return store.getAll();
  }

  async update(storeName, data) {
    const transaction = this.db.transaction([storeName], 'readwrite');
    const store = transaction.objectStore(storeName);
    return store.put(data);
  }

  async delete(storeName, key) {
    const transaction = this.db.transaction([storeName], 'readwrite');
    const store = transaction.objectStore(storeName);
    return store.delete(key);
  }

  async clear(storeName) {
    const transaction = this.db.transaction([storeName], 'readwrite');
    const store = transaction.objectStore(storeName);
    return store.clear();
  }

  async getAllByIndex(storeName, indexName, value) {
    const transaction = this.db.transaction([storeName], 'readonly');
    const store = transaction.objectStore(storeName);
    const index = store.index(indexName);
    return index.getAll(value);
  }
}

// Usage
const db = new PWADatabase();

async function savePost(post) {
  await db.init();
  const postData = {
    ...post,
    timestamp: Date.now(),
    synced: false
  };
  await db.add('posts', postData);
}

async function getUnsyncedPosts() {
  await db.init();
  return db.getAllByIndex('posts', 'synced', false);
}
```

### 7. Install Prompt

```javascript
// app.js - Handle install prompt

let deferredPrompt;

window.addEventListener('beforeinstallprompt', (event) => {
  // Prevent automatic prompt
  event.preventDefault();
  
  // Save event for later
  deferredPrompt = event;
  
  // Show custom install button
  showInstallButton();
});

function showInstallButton() {
  const installButton = document.getElementById('install-button');
  installButton.style.display = 'block';

  installButton.addEventListener('click', async () => {
    if (!deferredPrompt) return;

    // Show install prompt
    deferredPrompt.prompt();

    // Wait for user response
    const { outcome } = await deferredPrompt.userChoice;
    
    console.log(`User response: ${outcome}`);
    
    if (outcome === 'accepted') {
      console.log('PWA installed');
    } else {
      console.log('PWA installation declined');
    }

    // Clear the deferred prompt
    deferredPrompt = null;
    installButton.style.display = 'none';
  });
}

// Detect if already installed
window.addEventListener('appinstalled', () => {
  console.log('PWA was installed');
  // Hide install button
  document.getElementById('install-button').style.display = 'none';
  
  // Track analytics
  trackEvent('pwa_installed');
});

// Check if running as installed app
function isRunningStandalone() {
  return (
    window.matchMedia('(display-mode: standalone)').matches ||
    window.navigator.standalone || // iOS
    document.referrer.includes('android-app://')
  );
}

if (isRunningStandalone()) {
  console.log('Running as installed PWA');
} else {
  console.log('Running in browser');
}
```

### 8. Complete PWA Example

```javascript
// pwa-manager.js - Main PWA orchestration

class PWAManager {
  constructor() {
    this.db = null;
    this.swRegistration = null;
    this.isOnline = navigator.onLine;
    this.init();
  }

  async init() {
    // Initialize database
    this.db = new PWADatabase();
    await this.db.init();

    // Register service worker
    await this.registerServiceWorker();

    // Setup event listeners
    this.setupEventListeners();

    // Request notification permission
    await this.requestNotificationPermission();

    // Setup install prompt
    this.setupInstallPrompt();

    console.log('PWA Manager initialized');
  }

  async registerServiceWorker() {
    if ('serviceWorker' in navigator) {
      try {
        this.swRegistration = await navigator.serviceWorker.register('/sw.js');
        console.log('Service Worker registered');

        // Check for updates
        this.swRegistration.addEventListener('updatefound', () => {
          const newWorker = this.swRegistration.installing;
          newWorker.addEventListener('statechange', () => {
            if (newWorker.state === 'installed' && navigator.serviceWorker.controller) {
              // New service worker available
              this.showUpdateNotification();
            }
          });
        });
      } catch (error) {
        console.error('Service Worker registration failed:', error);
      }
    }
  }

  setupEventListeners() {
    // Online/Offline detection
    window.addEventListener('online', () => {
      this.isOnline = true;
      this.showNotification('Back online', 'Your connection has been restored');
      this.syncPendingData();
    });

    window.addEventListener('offline', () => {
      this.isOnline = false;
      this.showNotification('Offline mode', 'You can continue working offline');
    });

    // Visibility change
    document.addEventListener('visibilitychange', () => {
      if (!document.hidden && this.swRegistration) {
        this.swRegistration.update();
      }
    });
  }

  async requestNotificationPermission() {
    if ('Notification' in window && Notification.permission === 'default') {
      await Notification.requestPermission();
    }
  }

  setupInstallPrompt() {
    let deferredPrompt;

    window.addEventListener('beforeinstallprompt', (event) => {
      event.preventDefault();
      deferredPrompt = event;
      
      // Show install UI
      const installBtn = document.getElementById('install-btn');
      if (installBtn) {
        installBtn.style.display = 'block';
        installBtn.onclick = async () => {
          deferredPrompt.prompt();
          const { outcome } = await deferredPrompt.userChoice;
          console.log(`Install outcome: ${outcome}`);
          installBtn.style.display = 'none';
          deferredPrompt = null;
        };
      }
    });
  }

  async syncPendingData() {
    if (!this.isOnline) return;

    const pendingItems = await this.db.getAllByIndex('posts', 'synced', false);
    
    for (let item of pendingItems) {
      try {
        await fetch('/api/sync', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(item)
        });
        
        item.synced = true;
        await this.db.update('posts', item);
      } catch (error) {
        console.error('Sync failed for item:', item.id);
      }
    }
  }

  showNotification(title, body) {
    if ('Notification' in window && Notification.permission === 'granted') {
      if (this.swRegistration) {
        this.swRegistration.showNotification(title, {
          body,
          icon: '/icons/icon-192x192.png',
          badge: '/icons/badge-72x72.png'
        });
      } else {
        new Notification(title, { body });
      }
    }
  }

  showUpdateNotification() {
    this.showNotification(
      'Update available',
      'A new version is available. Refresh to update.'
    );
  }

  async saveData(data) {
    // Save to IndexedDB
    await this.db.add('posts', {
      ...data,
      timestamp: Date.now(),
      synced: this.isOnline
    });

    // Try to sync immediately if online
    if (this.isOnline) {
      try {
        await fetch('/api/save', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(data)
        });
      } catch (error) {
        console.error('Failed to sync immediately:', error);
      }
    } else {
      // Register background sync
      if ('sync' in this.swRegistration) {
        await this.swRegistration.sync.register('sync-data');
      }
    }
  }
}

// Initialize PWA
const pwaManager = new PWAManager();

// Export for use in other files
export default pwaManager;
```

### Role of JavaScript in PWAs - Summary

| Feature | JavaScript's Role |
|---------|------------------|
| **Service Workers** | Complete control - intercept network requests, cache management, background processing |
| **Offline Functionality** | Cache API, IndexedDB, offline/online detection |
| **Push Notifications** | Subscribe users, handle push events, show notifications |
| **Background Sync** | Queue operations, sync when online |
| **Install Experience** | Detect install prompt, customize install flow |
| **Performance** | Lazy loading, code splitting, resource optimization |
| **App Shell** | Load UI instantly, update dynamically |
| **Native Features** | Access camera, geolocation, sensors via JavaScript APIs |

### Best Practices for PWA JavaScript

1. **Progressive Enhancement** - Start with basic functionality, enhance with PWA features
2. **Cache Strategically** - Different strategies for different resource types
3. **Handle Offline Gracefully** - Provide meaningful offline experiences
4. **Update Service Workers** - Version your cache, clean up old versions
5. **Test Extensively** - Test offline scenarios, slow networks, edge cases
6. **Monitor Performance** - Track cache hit rates, sync success rates
7. **Secure Everything** - HTTPS required, validate all inputs
8. **Optimize Assets** - Minimize JavaScript, lazy load resources
9. **Provide Feedback** - Show loading states, sync status, connectivity
10. **Analytics** - Track PWA-specific metrics (installs, offline usage)

JavaScript is absolutely essential to PWAs - it powers the service worker, manages caching, enables offline functionality, handles push notifications, and creates the app-like experience that defines Progressive Web Apps.




# JavaScript and Mobile Development (98-100)
## 98. Explain how to use JavaScript for mobile development.

### Overview of JavaScript Mobile Development

JavaScript has evolved beyond the browser, becoming a powerful tool for building native and hybrid mobile applications across iOS and Android platforms.

### Mobile Development Approaches

```
┌─────────────────────────────────────────────┐
│     JavaScript Mobile Development           │
├─────────────────────────────────────────────┤
│  1. Native Apps (React Native, NativeScript)│
│  2. Hybrid Apps (Ionic, Cordova)           │
│  3. Progressive Web Apps (PWAs)             │
│  4. Cross-Platform (Flutter with JS bridge) │
└─────────────────────────────────────────────┘
```

### 1. React Native

**True Native Apps using JavaScript**

#### Setup and Basic Structure

```bash
# Install React Native CLI
npm install -g react-native-cli

# Create new project
npx react-native init MyMobileApp

# Run on iOS (requires Mac)
npx react-native run-ios

# Run on Android
npx react-native run-android
```

#### Basic React Native Components

```javascript
// App.js
import React, { useState } from 'react';
import {
  StyleSheet,
  Text,
  View,
  Button,
  TextInput,
  ScrollView,
  Image,
  TouchableOpacity,
  Alert,
  FlatList
} from 'react-native';

const App = () => {
  const [text, setText] = useState('');
  const [items, setItems] = useState([]);

  const addItem = () => {
    if (text.trim()) {
      setItems([...items, { id: Date.now().toString(), text }]);
      setText('');
    }
  };

  const deleteItem = (id) => {
    Alert.alert(
      'Delete Item',
      'Are you sure?',
      [
        { text: 'Cancel', style: 'cancel' },
        { 
          text: 'Delete', 
          style: 'destructive',
          onPress: () => setItems(items.filter(item => item.id !== id))
        }
      ]
    );
  };

  return (
    <View style={styles.container}>
      <Text style={styles.title}>My Todo App</Text>
      
      <View style={styles.inputContainer}>
        <TextInput
          style={styles.input}
          placeholder="Enter task"
          value={text}
          onChangeText={setText}
          onSubmitEditing={addItem}
        />
        <Button title="Add" onPress={addItem} />
      </View>

      <FlatList
        data={items}
        keyExtractor={(item) => item.id}
        renderItem={({ item }) => (
          <TouchableOpacity 
            style={styles.item}
            onPress={() => deleteItem(item.id)}
          >
            <Text style={styles.itemText}>{item.text}</Text>
          </TouchableOpacity>
        )}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    backgroundColor: '#f5f5f5',
  },
  title: {
    fontSize: 24,
    fontWeight: 'bold',
    marginTop: 40,
    marginBottom: 20,
    textAlign: 'center',
  },
  inputContainer: {
    flexDirection: 'row',
    marginBottom: 20,
  },
  input: {
    flex: 1,
    borderWidth: 1,
    borderColor: '#ddd',
    padding: 10,
    marginRight: 10,
    borderRadius: 5,
    backgroundColor: '#fff',
  },
  item: {
    padding: 15,
    backgroundColor: '#fff',
    borderRadius: 5,
    marginBottom: 10,
  },
  itemText: {
    fontSize: 16,
  },
});

export default App;
```

#### Navigation in React Native

```bash
# Install React Navigation
npm install @react-navigation/native
npm install @react-navigation/native-stack
npm install react-native-screens react-native-safe-area-context
```

```javascript
// Navigation.js
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';
import { View, Text, Button, StyleSheet } from 'react-native';

const Stack = createNativeStackNavigator();

// Home Screen
const HomeScreen = ({ navigation }) => {
  return (
    <View style={styles.screen}>
      <Text style={styles.title}>Home Screen</Text>
      <Button
        title="Go to Details"
        onPress={() => navigation.navigate('Details', { itemId: 42 })}
      />
    </View>
  );
};

// Details Screen
const DetailsScreen = ({ route, navigation }) => {
  const { itemId } = route.params;

  return (
    <View style={styles.screen}>
      <Text style={styles.title}>Details Screen</Text>
      <Text>Item ID: {itemId}</Text>
      <Button title="Go Back" onPress={() => navigation.goBack()} />
      <Button 
        title="Go to Settings" 
        onPress={() => navigation.navigate('Settings')} 
      />
    </View>
  );
};

// Settings Screen
const SettingsScreen = () => {
  return (
    <View style={styles.screen}>
      <Text style={styles.title}>Settings Screen</Text>
    </View>
  );
};

// Main App with Navigation
const App = () => {
  return (
    <NavigationContainer>
      <Stack.Navigator 
        initialRouteName="Home"
        screenOptions={{
          headerStyle: { backgroundColor: '#6200ee' },
          headerTintColor: '#fff',
          headerTitleStyle: { fontWeight: 'bold' },
        }}
      >
        <Stack.Screen 
          name="Home" 
          component={HomeScreen}
          options={{ title: 'My Home' }}
        />
        <Stack.Screen name="Details" component={DetailsScreen} />
        <Stack.Screen name="Settings" component={SettingsScreen} />
      </Stack.Navigator>
    </NavigationContainer>
  );
};

const styles = StyleSheet.create({
  screen: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    padding: 20,
  },
  title: {
    fontSize: 24,
    fontWeight: 'bold',
    marginBottom: 20,
  },
});

export default App;
```

#### Native Features Access

```javascript
// Camera Access
import { Camera } from 'react-native-camera';
import { launchCamera, launchImageLibrary } from 'react-native-image-picker';

const CameraComponent = () => {
  const [image, setImage] = useState(null);

  const openCamera = () => {
    launchCamera({ mediaType: 'photo', quality: 0.8 }, (response) => {
      if (!response.didCancel && !response.error) {
        setImage(response.assets[0].uri);
      }
    });
  };

  return (
    <View>
      <Button title="Take Photo" onPress={openCamera} />
      {image && <Image source={{ uri: image }} style={{ width: 200, height: 200 }} />}
    </View>
  );
};

// Geolocation
import Geolocation from '@react-native-community/geolocation';

const LocationComponent = () => {
  const [location, setLocation] = useState(null);

  const getLocation = () => {
    Geolocation.getCurrentPosition(
      (position) => {
        setLocation({
          latitude: position.coords.latitude,
          longitude: position.coords.longitude,
        });
      },
      (error) => console.error(error),
      { enableHighAccuracy: true, timeout: 20000, maximumAge: 1000 }
    );
  };

  return (
    <View>
      <Button title="Get Location" onPress={getLocation} />
      {location && (
        <Text>
          Lat: {location.latitude}, Long: {location.longitude}
        </Text>
      )}
    </View>
  );
};

// Local Storage
import AsyncStorage from '@react-native-async-storage/async-storage';

const StorageExample = () => {
  const saveData = async (key, value) => {
    try {
      await AsyncStorage.setItem(key, JSON.stringify(value));
      console.log('Data saved');
    } catch (error) {
      console.error('Error saving data:', error);
    }
  };

  const getData = async (key) => {
    try {
      const value = await AsyncStorage.getItem(key);
      return value ? JSON.parse(value) : null;
    } catch (error) {
      console.error('Error getting data:', error);
    }
  };

  return (
    <View>
      <Button 
        title="Save Data" 
        onPress={() => saveData('user', { name: 'John', age: 30 })} 
      />
      <Button 
        title="Get Data" 
        onPress={async () => {
          const data = await getData('user');
          console.log(data);
        }} 
      />
    </View>
  );
};

// Push Notifications
import PushNotification from 'react-native-push-notification';

const NotificationManager = {
  configure: () => {
    PushNotification.configure({
      onNotification: (notification) => {
        console.log('Notification received:', notification);
      },
      permissions: {
        alert: true,
        badge: true,
        sound: true,
      },
      popInitialNotification: true,
      requestPermissions: true,
    });
  },

  sendLocalNotification: (title, message) => {
    PushNotification.localNotification({
      title: title,
      message: message,
      playSound: true,
      soundName: 'default',
    });
  },

  scheduleNotification: (title, message, date) => {
    PushNotification.localNotificationSchedule({
      title: title,
      message: message,
      date: date,
    });
  },
};
```

### 2. Ionic Framework

**Hybrid Apps using Web Technologies**

#### Setup Ionic

```bash
# Install Ionic CLI
npm install -g @ionic/cli

# Create new app
ionic start myApp tabs --type=react

# Run in browser
ionic serve

# Build for mobile
ionic build

# Add platforms
ionic capacitor add ios
ionic capacitor add android

# Run on device
ionic capacitor run android
ionic capacitor run ios
```

#### Ionic React Components

```javascript
// Home.tsx
import React, { useState } from 'react';
import {
  IonContent,
  IonHeader,
  IonPage,
  IonTitle,
  IonToolbar,
  IonButton,
  IonInput,
  IonItem,
  IonLabel,
  IonList,
  IonCard,
  IonCardHeader,
  IonCardTitle,
  IonCardContent,
  IonIcon,
  IonAlert,
  IonToast,
} from '@ionic/react';
import { add, trash } from 'ionicons/icons';

const Home: React.FC = () => {
  const [task, setTask] = useState('');
  const [tasks, setTasks] = useState<string[]>([]);
  const [showAlert, setShowAlert] = useState(false);
  const [showToast, setShowToast] = useState(false);

  const addTask = () => {
    if (task.trim()) {
      setTasks([...tasks, task]);
      setTask('');
      setShowToast(true);
    }
  };

  const deleteTask = (index: number) => {
    setTasks(tasks.filter((_, i) => i !== index));
  };

  return (
    <IonPage>
      <IonHeader>
        <IonToolbar color="primary">
          <IonTitle>My Tasks</IonTitle>
        </IonToolbar>
      </IonHeader>

      <IonContent fullscreen>
        <IonCard>
          <IonCardHeader>
            <IonCardTitle>Add New Task</IonCardTitle>
          </IonCardHeader>
          <IonCardContent>
            <IonItem>
              <IonLabel position="floating">Task Description</IonLabel>
              <IonInput
                value={task}
                onIonChange={e => setTask(e.detail.value!)}
              />
            </IonItem>
            <IonButton expand="block" onClick={addTask}>
              <IonIcon slot="start" icon={add} />
              Add Task
            </IonButton>
          </IonCardContent>
        </IonCard>

        <IonList>
          {tasks.map((task, index) => (
            <IonItem key={index}>
              <IonLabel>{task}</IonLabel>
              <IonButton 
                fill="clear" 
                slot="end"
                onClick={() => deleteTask(index)}
              >
                <IonIcon icon={trash} />
              </IonButton>
            </IonItem>
          ))}
        </IonList>

        <IonToast
          isOpen={showToast}
          onDidDismiss={() => setShowToast(false)}
          message="Task added successfully"
          duration={2000}
          color="success"
        />

        <IonAlert
          isOpen={showAlert}
          onDidDismiss={() => setShowAlert(false)}
          header="Confirm"
          message="Are you sure you want to delete this task?"
          buttons={['Cancel', 'Delete']}
        />
      </IonContent>
    </IonPage>
  );
};

export default Home;
```

#### Ionic Native Plugins

```javascript
// Using Capacitor plugins
import { Camera, CameraResultType } from '@capacitor/camera';
import { Geolocation } from '@capacitor/geolocation';
import { Storage } from '@capacitor/storage';

// Camera
const takePicture = async () => {
  const image = await Camera.getPhoto({
    quality: 90,
    allowEditing: true,
    resultType: CameraResultType.Uri
  });

  const imageUrl = image.webPath;
  console.log(imageUrl);
};

// Geolocation
const getCurrentPosition = async () => {
  const coordinates = await Geolocation.getCurrentPosition();
  console.log('Current position:', coordinates);
};

// Storage
const saveToStorage = async (key: string, value: any) => {
  await Storage.set({
    key: key,
    value: JSON.stringify(value)
  });
};

const getFromStorage = async (key: string) => {
  const { value } = await Storage.get({ key: key });
  return value ? JSON.parse(value) : null;
};
```

### 3. NativeScript

**Another Native Approach with JavaScript**

```bash
# Install NativeScript CLI
npm install -g nativescript

# Create new app
ns create MyApp --template @nativescript/template-blank

# Run on device
ns run android
ns run ios
```

```javascript
// main-page.js
import { Observable } from '@nativescript/core';

export function onNavigatingTo(args) {
  const page = args.object;
  const viewModel = new Observable();
  
  viewModel.set('message', 'Hello NativeScript!');
  viewModel.set('counter', 0);
  
  viewModel.onTap = () => {
    const count = viewModel.get('counter');
    viewModel.set('counter', count + 1);
  };
  
  page.bindingContext = viewModel;
}
```

```xml
<!-- main-page.xml -->
<Page xmlns="http://schemas.nativescript.org/tns.xsd" navigatingTo="onNavigatingTo">
  <StackLayout>
    <Label text="{{ message }}" class="title" />
    <Label text="{{ 'Count: ' + counter }}" />
    <Button text="Tap Me" tap="{{ onTap }}" />
  </StackLayout>
</Page>
```

### 4. Apache Cordova / PhoneGap

**Classic Hybrid Approach**

```bash
# Install Cordova
npm install -g cordova

# Create project
cordova create myApp com.example.myapp MyApp

# Add platforms
cordova platform add android
cordova platform add ios

# Add plugins
cordova plugin add cordova-plugin-camera
cordova plugin add cordova-plugin-geolocation

# Build and run
cordova build android
cordova run android
```

```javascript
// Using Cordova plugins
document.addEventListener('deviceready', onDeviceReady, false);

function onDeviceReady() {
  console.log('Device is ready');

  // Camera
  navigator.camera.getPicture(
    (imageData) => {
      const image = document.getElementById('myImage');
      image.src = 'data:image/jpeg;base64,' + imageData;
    },
    (error) => console.error('Camera error:', error),
    {
      quality: 50,
      destinationType: Camera.DestinationType.DATA_URL
    }
  );

  // Geolocation
  navigator.geolocation.getCurrentPosition(
    (position) => {
      console.log('Lat:', position.coords.latitude);
      console.log('Long:', position.coords.longitude);
    },
    (error) => console.error('Location error:', error)
  );
}
```

### 5. Complete Mobile App Example

```javascript
// MobileApp.js - Full-featured React Native app

import React, { useState, useEffect } from 'react';
import {
  StyleSheet,
  Text,
  View,
  FlatList,
  TouchableOpacity,
  TextInput,
  Alert,
  ActivityIndicator,
  RefreshControl,
  Platform,
} from 'react-native';
import AsyncStorage from '@react-native-async-storage/async-storage';
import NetInfo from '@react-native-community/netinfo';

const MobileApp = () => {
  const [tasks, setTasks] = useState([]);
  const [text, setText] = useState('');
  const [loading, setLoading] = useState(false);
  const [refreshing, setRefreshing] = useState(false);
  const [isConnected, setIsConnected] = useState(true);

  // Load tasks from storage on mount
  useEffect(() => {
    loadTasks();
    
    // Monitor network connectivity
    const unsubscribe = NetInfo.addEventListener(state => {
      setIsConnected(state.isConnected);
      if (state.isConnected) {
        syncTasks();
      }
    });

    return () => unsubscribe();
  }, []);

  // Save tasks to storage whenever they change
  useEffect(() => {
    saveTasks();
  }, [tasks]);

  const loadTasks = async () => {
    try {
      setLoading(true);
      const storedTasks = await AsyncStorage.getItem('tasks');
      if (storedTasks) {
        setTasks(JSON.parse(storedTasks));
      }
    } catch (error) {
      console.error('Error loading tasks:', error);
    } finally {
      setLoading(false);
    }
  };

  const saveTasks = async () => {
    try {
      await AsyncStorage.setItem('tasks', JSON.stringify(tasks));
    } catch (error) {
      console.error('Error saving tasks:', error);
    }
  };

  const addTask = () => {
    if (text.trim()) {
      const newTask = {
        id: Date.now().toString(),
        text: text.trim(),
        completed: false,
        synced: isConnected,
        createdAt: new Date().toISOString(),
      };
      
      setTasks([newTask, ...tasks]);
      setText('');

      if (isConnected) {
        syncTaskToServer(newTask);
      }
    }
  };

  const toggleTask = (id) => {
    setTasks(tasks.map(task => 
      task.id === id 
        ? { ...task, completed: !task.completed, synced: false }
        : task
    ));
  };

  const deleteTask = (id) => {
    Alert.alert(
      'Delete Task',
      'Are you sure you want to delete this task?',
      [
        { text: 'Cancel', style: 'cancel' },
        {
          text: 'Delete',
          style: 'destructive',
          onPress: () => setTasks(tasks.filter(task => task.id !== id))
        }
      ]
    );
  };

  const syncTaskToServer = async (task) => {
    try {
      const response = await fetch('https://api.example.com/tasks', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(task),
      });

      if (response.ok) {
        setTasks(tasks.map(t => 
          t.id === task.id ? { ...t, synced: true } : t
        ));
      }
    } catch (error) {
      console.error('Sync error:', error);
    }
  };

  const syncTasks = async () => {
    const unsyncedTasks = tasks.filter(task => !task.synced);
    
    for (let task of unsyncedTasks) {
      await syncTaskToServer(task);
    }
  };

  const onRefresh = async () => {
    setRefreshing(true);
    await loadTasks();
    if (isConnected) {
      await syncTasks();
    }
    setRefreshing(false);
  };

  const renderTask = ({ item }) => (
    <TouchableOpacity 
      style={[styles.task, item.completed && styles.taskCompleted]}
      onPress={() => toggleTask(item.id)}
      onLongPress={() => deleteTask(item.id)}
    >
      <View style={styles.taskContent}>
        <Text style={[styles.taskText, item.completed && styles.taskTextCompleted]}>
          {item.text}
        </Text>
        {!item.synced && (
          <View style={styles.unsyncedIndicator}>
            <Text style={styles.unsyncedText}>⚠</Text>
          </View>
        )}
      </View>
    </TouchableOpacity>
  );

  if (loading) {
    return (
      <View style={styles.centerContainer}>
        <ActivityIndicator size="large" color="#6200ee" />
        <Text style={styles.loadingText}>Loading tasks...</Text>
      </View>
    );
  }

  return (
    <View style={styles.container}>
      <View style={styles.header}>
        <Text style={styles.title}>My Tasks</Text>
        {!isConnected && (
          <View style={styles.offlineBanner}>
            <Text style={styles.offlineText}>Offline Mode</Text>
          </View>
        )}
      </View>

      <View style={styles.inputContainer}>
        <TextInput
          style={styles.input}
          placeholder="Enter a new task"
          value={text}
          onChangeText={setText}
          onSubmitEditing={addTask}
          returnKeyType="done"
        />
        <TouchableOpacity style={styles.addButton} onPress={addTask}>
          <Text style={styles.addButtonText}>+</Text>
        </TouchableOpacity>
      </View>

      <FlatList
        data={tasks}
        renderItem={renderTask}
        keyExtractor={(item) => item.id}
        contentContainerStyle={styles.list}
        refreshControl={
          <RefreshControl refreshing={refreshing} onRefresh={onRefresh} />
        }
        ListEmptyComponent={() => (
          <View style={styles.emptyContainer}>
            <Text style={styles.emptyText}>No tasks yet. Add one above!</Text>
          </View>
        )}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#f5f5f5',
  },
  centerContainer: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  header: {
    backgroundColor: '#6200ee',
    padding: 20,
    paddingTop: Platform.OS === 'ios' ? 60 : 40,
  },
  title: {
    fontSize: 28,
    fontWeight: 'bold',
    color: '#fff',
  },
  offlineBanner: {
    marginTop: 10,
    padding: 8,
    backgroundColor: '#ff9800',
    borderRadius: 4,
  },
  offlineText: {
    color: '#fff',
    fontWeight: 'bold',
    textAlign: 'center',
  },
  inputContainer: {
    flexDirection: 'row',
    padding: 15,
    backgroundColor: '#fff',
    borderBottomWidth: 1,
    borderBottomColor: '#e0e0e0',
  },
  input: {
    flex: 1,
    height: 45,
    borderWidth: 1,
    borderColor: '#ddd',
    borderRadius: 8,
    paddingHorizontal: 15,
    fontSize: 16,
    backgroundColor: '#f9f9f9',
  },
  addButton: {
    width: 45,
    height: 45,
    backgroundColor: '#6200ee',
    borderRadius: 8,
    justifyContent: 'center',
    alignItems: 'center',
    marginLeft: 10,
  },
  addButtonText: {
    color: '#fff',
    fontSize: 24,
    fontWeight: 'bold',
  },
  list: {
    padding: 15,
  },
  task: {
    backgroundColor: '#fff',
    padding: 15,
    borderRadius: 8,
    marginBottom: 10,
    flexDirection: 'row',
    alignItems: 'center',
    elevation: 2,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.1,
    shadowRadius: 4,
  },
  taskCompleted: {
    opacity: 0.6,
    backgroundColor: '#e8f5e9',
  },
  taskContent: {
    flex: 1,
    flexDirection: 'row',
    justifyContent: 'space-between',
    alignItems: 'center',
  },
  taskText: {
    fontSize: 16,
    flex: 1,
  },
  taskTextCompleted: {
    textDecorationLine: 'line-through',
    color: '#666',
  },
  unsyncedIndicator: {
    marginLeft: 10,
  },
  unsyncedText: {
    fontSize: 18,
    color: '#ff9800',
  },
  emptyContainer: {
    padding: 40,
    alignItems: 'center',
  },
  emptyText: {
    fontSize: 16,
    color: '#999',
    textAlign: 'center',
  },
  loadingText: {
    marginTop: 10,
    fontSize: 16,
    color: '#666',
  },
});

export default MobileApp;
```

### Comparison of Approaches

| Approach | Performance | Native Features | Development | UI/UX |
|----------|-------------|-----------------|-------------|-------|
| **React Native** | Near-native | Full access | JavaScript/React | Native components |
| **Ionic** | Web-based | Via plugins | HTML/CSS/JS | Web-based |
| **NativeScript** | Native | Full access | JavaScript/XML | Native components |
| **Cordova** | Web-based | Via plugins | HTML/CSS/JS | Web-based |
| **PWA** | Web-based | Limited | HTML/CSS/JS | Web-based |

### Best Practices

1. **Optimize Performance** - Lazy load components, minimize re-renders
2. **Handle Offline** - Cache data, sync when online
3. **Test on Real Devices** - Emulators don't show everything
4. **Platform-Specific Code** - Use Platform.select() when needed
5. **Accessibility** - Support screen readers, proper labeling
6. **Security** - Secure storage, API authentication
7. **Updates** - Use CodePush or similar for over-the-air updates
8. **Analytics** - Track user behavior, crashes
9. **Responsive Design** - Support different screen sizes
10. **Native Modules** - Write platform-specific code when necessary

---

## 99. What is React Native and how does it differ from traditional web apps?

### What is React Native?

**React Native** is an open-source framework created by Facebook (Meta) that allows developers to build mobile applications for iOS and Android using JavaScript and React. Unlike traditional web apps, React Native apps are **truly native** applications.

```
┌──────────────────────────────────────────┐
│          React Native Architecture       │
├──────────────────────────────────────────┤
│  JavaScript Code (React Components)      │
│              ↓                            │
│         Bridge                            │
│              ↓                            │
│  Native Modules (iOS/Android)            │
│              ↓                            │
│  Native UI Components                    │
└──────────────────────────────────────────┘
```

### Key Differences from Traditional Web Apps

#### 1. **Rendering Engine**

**Traditional Web App:**
```javascript
// Web app - renders to DOM
import React from 'react';

function WebApp() {
  return (
    <div className="container">
      <h1>Hello Web</h1>
      <button onClick={handleClick}>Click me</button>
    </div>
  );
}

// Renders to: <div>, <h1>, <button> HTML elements
```

**React Native:**
```javascript
// React Native - renders to native components
import React from 'react';
import { View, Text, TouchableOpacity, StyleSheet } from 'react-native';

function NativeApp() {
  return (
    <View style={styles.container}>
      <Text style={styles.title}>Hello Native</Text>
      <TouchableOpacity onPress={handleClick}>
        <Text>Click me</Text>
      </TouchableOpacity>
    </View>
  );
}

// Renders to: UIView, UILabel, UIButton (iOS) or 
// View, TextView, Button (Android)
```

#### 2. **Styling Approach**

**Web CSS:**
```css
/* styles.css */
.container {
  display: flex;
  flex-direction: column;
  background-color: #fff;
  padding: 20px;
}

.title {
  font-size: 24px;
  font-weight: bold;
  color: #333;
}
```

**React Native StyleSheet:**
```javascript
// No CSS files - styles in JavaScript
import { StyleSheet } from 'react-native';

const styles = StyleSheet.create({
  container: {
    flex: 1,
    flexDirection: 'column',
    backgroundColor: '#fff',
    padding: 20,
  },
  title: {
    fontSize: 24,
    fontWeight: 'bold',
    color: '#333',
  },
});

// Key differences:
// - No units (numbers are dp/pt)
// - No cascading
// - CamelCase properties (backgroundColor not background-color)
// - Subset of CSS properties
// - Flexbox by default
```

#### 3. **Component Comparison**

| Web (HTML/React) | React Native | Native Equivalent |
|------------------|--------------|-------------------|
| `<div>` | `<View>` | UIView (iOS), ViewGroup (Android) |
| `<span>`, `<p>` | `<Text>` | UILabel (iOS), TextView (Android) |
| `<img>` | `<Image>` | UIImageView (iOS), ImageView (Android) |
| `<input>` | `<TextInput>` | UITextField (iOS), EditText (Android) |
| `<button>` | `<TouchableOpacity>`, `<Button>` | UIButton (iOS), Button (Android) |
| `<ul>`, `<ol>` | `<FlatList>`, `<SectionList>` | UITableView (iOS), RecyclerView (Android) |
| `<a>` | Custom with navigation | - |
| `<video>` | `<Video>` (third-party) | AVPlayer (iOS), MediaPlayer (Android) |

#### 4. **Navigation**

**Web App (React Router):**
```javascript
import { BrowserRouter, Routes, Route, Link } from 'react-router-dom';

function WebNavigation() {
  return (
    <BrowserRouter>
      <nav>
        <Link to="/">Home</Link>
        <Link to="/profile">Profile</Link>
      </nav>
      
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/profile" element={<Profile />} />
      </Routes>
    </BrowserRouter>
  );
}
```

**React Native (React Navigation):**
```javascript
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';

const Stack = createNativeStackNavigator();

function NativeNavigation() {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen name="Home" component={Home} />
        <Stack.Screen name="Profile" component={Profile} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}

// Navigation:
// navigation.navigate('Profile');
// navigation.goBack();
// navigation.push('Details');
```

#### 5. **Layout System**

**Web App:**
```javascript
// Multiple layout options: Flexbox, Grid, Float, Position
function WebLayout() {
  return (
    <div style={{
      display: 'grid',
      gridTemplateColumns: '1fr 2fr',
      gap: '20px'
    }}>
      <aside>Sidebar</aside>
      <main>Content</main>
    </div>
  );
}
```

**React Native:**
```javascript
// Primarily Flexbox (no CSS Grid)
function NativeLayout() {
  return (
    <View style={{
      flex: 1,
      flexDirection: 'row'
    }}>
      <View style={{ flex: 1 }}>
        <Text>Sidebar</Text>
      </View>
      <View style={{ flex: 2 }}>
        <Text>Content</Text>
      </View>
    </View>
  );
}
```

### Core React Native Concepts

#### 1. **Bridge Architecture**

```
JavaScript Thread          Bridge          Native Thread
─────────────────          ──────          ─────────────
React Components    ←──→  JSON Messages  ←──→  Native UI
State Management    ←──→  Serialization  ←──→  Platform APIs
Event Handlers      ←──→  Async Comm.    ←──→  Sensors, Camera
```

**How it works:**
```javascript
// JavaScript side
import { NativeModules } from 'react-native';

// Call native module
NativeModules.CalendarModule.createEvent('Party', 'My House')
  .then(eventId => console.log(`Event created: ${eventId}`))
  .catch(error => console.error(error));

// Native side receives JSON message
// Executes native code
// Returns result via bridge
```

#### 2. **Platform-Specific Code**

**Method 1: Platform module**
```javascript
import { Platform, StyleSheet } from 'react-native';

const styles = StyleSheet.create({
  container: {
    padding: Platform.OS === 'ios' ? 20 : 10,
    marginTop: Platform.select({
      ios: 0,
      android: 25,
      default: 0
    })
  }
});

// Check platform version
if (Platform.Version > 28) {
  // Android API level > 28
}
```

**Method 2: Platform-specific files**
```javascript
// Button.ios.js
import React from 'react';
import { StyleSheet } from 'react-native';

export const Button = ({ title }) => (
  <TouchableOpacity style={styles.iosButton}>
    <Text>{title}</Text>
  </TouchableOpacity>
);

// Button.android.js
export const Button = ({ title }) => (
  <TouchableOpacity style={styles.androidButton}>
    <Text>{title}</Text>
  </TouchableOpacity>
);

// Import automatically selects correct file
import { Button } from './Button';
```

#### 3. **Native Modules**

**Creating a Custom Native Module (iOS):**

```objective-c
// CalendarManager.h
#import <React/RCTBridgeModule.h>

@interface CalendarManager : NSObject <RCTBridgeModule>
@end

// CalendarManager.m
#import "CalendarManager.h"
#import <React/RCTLog.h>

@implementation CalendarManager

RCT_EXPORT_MODULE();

RCT_EXPORT_METHOD(addEvent:(NSString *)name location:(NSString *)location)
{
  RCTLogInfo(@"Pretending to create an event %@ at %@", name, location);
}

RCT_EXPORT_METHOD(findEvents:(RCTPromiseResolveBlock)resolve
                  rejecter:(RCTPromiseRejectBlock)reject)
{
  NSArray *events = @[@"Event 1", @"Event 2"];
  resolve(events);
}

@end
```

**Using in JavaScript:**
```javascript
import { NativeModules } from 'react-native';

const { CalendarManager } = NativeModules;

// Call native method
CalendarManager.addEvent('Birthday Party', 'My House');

// With promise
CalendarManager.findEvents()
  .then(events => console.log(events))
  .catch(error => console.error(error));
```

### Performance Differences

#### Web App Performance Issues:
```javascript
// DOM manipulation can be slow
for (let i = 0; i < 1000; i++) {
  const element = document.createElement('div');
  element.textContent = `Item ${i}`;
  document.body.appendChild(element); // Causes reflow each time
}
```

#### React Native Optimization:
```javascript
// FlatList virtualizes rendering
<FlatList
  data={largeArray}
  renderItem={({ item }) => <ItemComponent item={item} />}
  keyExtractor={item => item.id}
  // Only renders visible items + buffer
  initialNumToRender={10}
  maxToRenderPerBatch={10}
  windowSize={5}
  removeClippedSubviews={true}
/>
```

### Feature Comparison

#### 1. **Access to Device Features**

**Web App (Limited):**
```javascript
// Limited API access
// Camera (with getUserMedia)
navigator.mediaDevices.getUserMedia({ video: true })
  .then(stream => {
    video.srcObject = stream;
  });

// Geolocation
navigator.geolocation.getCurrentPosition(position => {
  console.log(position.coords.latitude);
});

// No access to: Contacts, Calendar, Bluetooth, NFC, etc.
```

**React Native (Full Access):**
```javascript
// Camera with full control
import { Camera } from 'react-native-camera';

<Camera
  style={styles.preview}
  type={Camera.Constants.Type.back}
  flashMode={Camera.Constants.FlashMode.on}
/>

// Contacts
import Contacts from 'react-native-contacts';

Contacts.getAll().then(contacts => {
  console.log(contacts);
});

// Bluetooth
import BleManager from 'react-native-ble-manager';

BleManager.scan([], 5, true).then(() => {
  console.log('Scanning...');
});

// File system
import RNFS from 'react-native-fs';

RNFS.readFile(path).then(contents => {
  console.log(contents);
});
```

#### 2. **Gestures and Animations**

**Web App:**
```javascript
// CSS animations
<div className="animated-box" />

/* CSS */
.animated-box {
  animation: slide 0.3s ease-in-out;
}

@keyframes slide {
  from { transform: translateX(-100px); }
  to { transform: translateX(0); }
}

// JavaScript animations (limited)
element.animate([
  { transform: 'translateX(0)' },
  { transform: 'translateX(100px)' }
], 300);
```

**React Native:**
```javascript
import { Animated, PanResponder } from 'react-native';

const AnimatedComponent = () => {
  const pan = useRef(new Animated.ValueXY()).current;
  const fadeAnim = useRef(new Animated.Value(0)).current;

  // Gesture handling
  const panResponder = PanResponder.create({
    onMoveShouldSetPanResponder: () => true,
    onPanResponderMove: Animated.event([
      null,
      { dx: pan.x, dy: pan.y }
    ], { useNativeDriver: false }),
    onPanResponderRelease: () => {
      Animated.spring(pan, {
        toValue: { x: 0, y: 0 },
        useNativeDriver: true
      }).start();
    }
  });

  // Native-driven animation (60fps)
  useEffect(() => {
    Animated.timing(fadeAnim, {
      toValue: 1,
      duration: 1000,
      useNativeDriver: true // Runs on native thread!
    }).start();
  }, []);

  return (
    <Animated.View
      {...panResponder.panHandlers}
      style={{
        transform: [
          { translateX: pan.x },
          { translateY: pan.y }
        ],
        opacity: fadeAnim
      }}
    >
      <Text>Drag me!</Text>
    </Animated.View>
  );
};
```

#### 3. **Storage**

**Web App:**
```javascript
// localStorage (5-10MB limit)
localStorage.setItem('user', JSON.stringify(user));

// IndexedDB (larger storage)
const db = await openDB('my-db', 1);
await db.put('users', user);

// Cookies (4KB limit)
document.cookie = "username=John";
```

**React Native:**
```javascript
// AsyncStorage (unlimited, async)
import AsyncStorage from '@react-native-async-storage/async-storage';

await AsyncStorage.setItem('user', JSON.stringify(user));
const user = JSON.parse(await AsyncStorage.getItem('user'));

// Encrypted storage
import EncryptedStorage from 'react-native-encrypted-storage';

await EncryptedStorage.setItem('token', 'secret-token');

// Realm Database (complex data)
import Realm from 'realm';

const UserSchema = {
  name: 'User',
  properties: {
    id: 'int',
    name: 'string',
    age: 'int'
  }
};

const realm = await Realm.open({ schema: [UserSchema] });
```

### Complete Comparison Example

**Web App:**
```javascript
// Web version
import React, { useState, useEffect } from 'react';
import './App.css';

function TodoApp() {
  const [todos, setTodos] = useState([]);
  const [text, setText] = useState('');

  useEffect(() => {
    const saved = localStorage.getItem('todos');
    if (saved) setTodos(JSON.parse(saved));
  }, []);

  useEffect(() => {
    localStorage.setItem('todos', JSON.stringify(todos));
  }, [todos]);

  const addTodo = () => {
    setTodos([...todos, { id: Date.now(), text, done: false }]);
    setText('');
  };

  return (
    <div className="app">
      <h1>Todo List</h1>
      <div className="input-container">
        <input
          type="text"
          value={text}
          onChange={e => setText(e.target.value)}
          onKeyPress={e => e.key === 'Enter' && addTodo()}
        />
        <button onClick={addTodo}>Add</button>
      </div>
      <ul className="todo-list">
        {todos.map(todo => (
          <li 
            key={todo.id}
            className={todo.done ? 'done' : ''}
            onClick={() => {
              setTodos(todos.map(t => 
                t.id === todo.id ? { ...t, done: !t.done } : t
              ));
            }}
          >
            {todo.text}
          </li>
        ))}
      </ul>
    </div>
  );
}
```

**React Native Version:**
```javascript
// React Native version
import React, { useState, useEffect } from 'react';
import {
  View,
  Text,
  TextInput,
  TouchableOpacity,
  FlatList,
  StyleSheet
} from 'react-native';
import AsyncStorage from '@react-native-async-storage/async-storage';

function TodoApp() {
  const [todos, setTodos] = useState([]);
  const [text, setText] = useState('');

  useEffect(() => {
    loadTodos();
  }, []);

  useEffect(() => {
    saveTodos();
  }, [todos]);

  const loadTodos = async () => {
    const saved = await AsyncStorage.getItem('todos');
    if (saved) setTodos(JSON.parse(saved));
  };

  const saveTodos = async () => {
    await AsyncStorage.setItem('todos', JSON.stringify(todos));
  };

  const addTodo = () => {
    setTodos([...todos, { id: Date.now().toString(), text, done: false }]);
    setText('');
  };

  return (
    <View style={styles.app}>
      <Text style={styles.title}>Todo List</Text>
      <View style={styles.inputContainer}>
        <TextInput
          style={styles.input}
          value={text}
          onChangeText={setText}
          onSubmitEditing={addTodo}
          placeholder="Enter todo"
        />
        <TouchableOpacity style={styles.button} onPress={addTodo}>
          <Text style={styles.buttonText}>Add</Text>
        </TouchableOpacity>
      </View>
      <FlatList
        data={todos}
        keyExtractor={item => item.id}
        renderItem={({ item }) => (
          <TouchableOpacity
            style={[styles.todoItem, item.done && styles.todoDone]}
            onPress={() => {
              setTodos(todos.map(t => 
                t.id === item.id ? { ...t, done: !t.done } : t
              ));
            }}
          >
            <Text style={[styles.todoText, item.done && styles.todoTextDone]}>
              {item.text}
            </Text>
          </TouchableOpacity>
        )}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  app: {
    flex: 1,
    padding: 20,
    paddingTop: 60,
    backgroundColor: '#f5f5f5',
  },
  title: {
    fontSize: 28,
    fontWeight: 'bold',
    marginBottom: 20,
  },
  inputContainer: {
    flexDirection: 'row',
    marginBottom: 20,
  },
  input: {
    flex: 1,
    height: 45,
    borderWidth: 1,
    borderColor: '#ddd',
    borderRadius: 8,
    paddingHorizontal: 15,
    backgroundColor: '#fff',
  },
  button: {
    marginLeft: 10,
    backgroundColor: '#007AFF',
    paddingHorizontal: 20,
    borderRadius: 8,
    justifyContent: 'center',
  },
  buttonText: {
    color: '#fff',
    fontWeight: 'bold',
  },
  todoItem: {
    padding: 15,
    backgroundColor: '#fff',
    borderRadius: 8,
    marginBottom: 10,
  },
  todoDone: {
    backgroundColor: '#e8f5e9',
  },
  todoText: {
    fontSize: 16,
  },
  todoTextDone: {
    textDecorationLine: 'line-through',
    color: '#999',
  },
});
```

### Advantages of React Native

1. **True Native Performance** - Native UI components, not web views
2. **Native Look & Feel** - Follows platform design guidelines
3. **Full Device Access** - Camera, sensors, Bluetooth, etc.
4. **Code Reusability** - Share code between iOS and Android (60-90%)
5. **Hot Reloading** - See changes instantly during development
6. **Large Ecosystem** - Extensive libraries and community
7. **Cost-Effective** - One codebase for multiple platforms
8. **React Knowledge** - Leverage existing React skills

### Disadvantages of React Native

1. **Bridge Overhead** - Communication between JS and native can be slow
2. **Limited CSS** - Subset of CSS properties, no CSS Grid
3. **Platform Differences** - Sometimes need platform-specific code
4. **Native Knowledge Needed** - Complex features may require native code
5. **App Size** - Larger than pure native apps
6. **Third-Party Dependencies** - Rely on community libraries
7. **Debugging Complexity** - JavaScript and native code debugging

### When to Use Each

**Use Web App When:**
- SEO is critical
- Cross-platform across all devices (desktop, mobile, tablet)
- Frequent updates needed
- Simple functionality
- Limited budget

**Use React Native When:**
- Native performance required
- Need device features (camera, GPS, sensors)
- Offline functionality crucial
- App store distribution
- Native look and feel important
- Complex animations and gestures

### Summary

| Aspect | Web App | React Native |
|--------|---------|--------------|
| **Technology** | HTML/CSS/JS | JavaScript + Native |
| **Rendering** | DOM | Native Components |
| **Performance** | Good | Excellent |
| **Device Access** | Limited | Full |
| **Distribution** | URL | App Stores |
| **Updates** | Instant | App Store Review |
| **Development** | Faster initial | More complex |
| **User Experience** | Web-like | Native-like |

React Native bridges the gap between web development and native mobile apps, allowing JavaScript developers to build performant, native mobile applications while maintaining much of the development experience they're familiar with from web development.




## 100. How does JavaScript interact with native mobile components?

### Overview

JavaScript interacts with native mobile components through a **bridge mechanism** that enables bidirectional communication between JavaScript code and platform-specific native code (Objective-C/Swift for iOS, Java/Kotlin for Android).

```
┌─────────────────────────────────────────────────────────────┐
│                    JavaScript Layer                         │
│  (React Native, Ionic, Cordova, NativeScript)              │
└──────────────────────┬──────────────────────────────────────┘
                       │
                   Bridge/FFI
                       │
┌──────────────────────┴──────────────────────────────────────┐
│                   Native Layer                              │
│  iOS (Objective-C/Swift)  |  Android (Java/Kotlin)         │
└─────────────────────────────────────────────────────────────┘
```

### 1. React Native Bridge Architecture

#### How the Bridge Works

```
JavaScript Thread          Bridge          Native Thread
─────────────────          ──────          ─────────────
• React Components    ←→   JSON     ←→    • Native Modules
• Business Logic      ←→   Messages ←→    • UI Components  
• Event Handlers      ←→   Async    ←→    • Platform APIs
• State Management    ←→   Batched  ←→    • Sensors, Camera
```

**Key Concepts:**
- **Asynchronous** - All communication is async
- **Serializable** - Data must be JSON-serializable
- **Batched** - Multiple messages batched for efficiency
- **Unidirectional** - Messages flow one way at a time

#### Bridge Communication Example

```javascript
// JavaScript side
import { NativeModules, NativeEventEmitter } from 'react-native';

const { MyNativeModule } = NativeModules;

// Call native method
MyNativeModule.processData({ id: 123, value: 'test' })
  .then(result => {
    console.log('Native returned:', result);
  })
  .catch(error => {
    console.error('Native error:', error);
  });

// Listen to native events
const eventEmitter = new NativeEventEmitter(MyNativeModule);
const subscription = eventEmitter.addListener(
  'DataProcessed',
  (event) => {
    console.log('Event from native:', event);
  }
);

// Clean up
subscription.remove();
```

### 2. Creating Native Modules

#### iOS Native Module (Objective-C)

**CalendarModule.h**
```objective-c
#import <React/RCTBridgeModule.h>
#import <React/RCTEventEmitter.h>

@interface CalendarModule : RCTEventEmitter <RCTBridgeModule>
@end
```

**CalendarModule.m**
```objective-c
#import "CalendarModule.h"
#import <React/RCTLog.h>

@implementation CalendarModule

// Export module to JavaScript
RCT_EXPORT_MODULE();

// Export method with parameters
RCT_EXPORT_METHOD(createEvent:(NSString *)name 
                  location:(NSString *)location 
                  date:(nonnull NSNumber *)date)
{
  RCTLogInfo(@"Creating event: %@ at %@", name, location);
  
  // Native iOS code here
  dispatch_async(dispatch_get_main_queue(), ^{
    // Update UI on main thread
    NSLog(@"Event created");
  });
}

// Method with callback
RCT_EXPORT_METHOD(findEvents:(RCTResponseSenderBlock)callback)
{
  NSArray *events = @[@{@"name": @"Meeting", @"date": @"2024-01-01"}];
  callback(@[[NSNull null], events]); // [error, result]
}

// Method with Promise
RCT_EXPORT_METHOD(getEventById:(NSString *)eventId
                  resolver:(RCTPromiseResolveBlock)resolve
                  rejecter:(RCTPromiseRejectBlock)reject)
{
  if (eventId.length > 0) {
    NSDictionary *event = @{
      @"id": eventId,
      @"name": @"Birthday Party",
      @"date": @"2024-12-25"
    };
    resolve(event);
  } else {
    NSError *error = [NSError errorWithDomain:@"CalendarModule" 
                                         code:404 
                                     userInfo:@{@"message": @"Event not found"}];
    reject(@"not_found", @"Event not found", error);
  }
}

// Send events to JavaScript
- (NSArray<NSString *> *)supportedEvents
{
  return @[@"EventCreated", @"EventDeleted"];
}

- (void)sendEventToJS
{
  [self sendEventWithName:@"EventCreated" 
                     body:@{@"eventId": @"123", @"name": @"New Event"}];
}

// Export constants
- (NSDictionary *)constantsToExport
{
  return @{
    @"DEFAULT_EVENT_COLOR": @"blue",
    @"MAX_ATTENDEES": @100
  };
}

// Runs on main queue (UI thread)
+ (BOOL)requiresMainQueueSetup
{
  return YES;
}

@end
```

#### iOS Native Module (Swift)

**CalendarModule.swift**
```swift
import Foundation
import React

@objc(CalendarModule)
class CalendarModule: RCTEventEmitter {
  
  // Export module
  @objc
  override static func moduleName() -> String! {
    return "CalendarModule"
  }
  
  // Export method
  @objc
  func createEvent(_ name: String, location: String, date: NSNumber) {
    print("Creating event: \(name) at \(location)")
    
    // Native Swift code
    DispatchQueue.main.async {
      // UI updates
    }
  }
  
  // Method with Promise
  @objc
  func getEventById(_ eventId: String,
                    resolver resolve: @escaping RCTPromiseResolveBlock,
                    rejecter reject: @escaping RCTPromiseRejectBlock) {
    if !eventId.isEmpty {
      let event: [String: Any] = [
        "id": eventId,
        "name": "Birthday Party",
        "date": "2024-12-25"
      ]
      resolve(event)
    } else {
      let error = NSError(domain: "CalendarModule", 
                         code: 404, 
                         userInfo: ["message": "Event not found"])
      reject("not_found", "Event not found", error)
    }
  }
  
  // Supported events
  @objc
  override func supportedEvents() -> [String]! {
    return ["EventCreated", "EventDeleted"]
  }
  
  // Send event to JS
  @objc
  func sendEventToJS() {
    sendEvent(withName: "EventCreated", 
              body: ["eventId": "123", "name": "New Event"])
  }
  
  // Export constants
  @objc
  override func constantsToExport() -> [AnyHashable : Any]! {
    return [
      "DEFAULT_EVENT_COLOR": "blue",
      "MAX_ATTENDEES": 100
    ]
  }
  
  @objc
  override static func requiresMainQueueSetup() -> Bool {
    return true
  }
}
```

**CalendarModule-Bridging-Header.h**
```objective-c
#import <React/RCTBridgeModule.h>
#import <React/RCTEventEmitter.h>
```

**CalendarModule.m (bridge)**
```objective-c
#import <React/RCTBridgeModule.h>

@interface RCT_EXTERN_MODULE(CalendarModule, RCTEventEmitter)

RCT_EXTERN_METHOD(createEvent:(NSString *)name 
                  location:(NSString *)location 
                  date:(nonnull NSNumber *)date)

RCT_EXTERN_METHOD(getEventById:(NSString *)eventId
                  resolver:(RCTPromiseResolveBlock)resolve
                  rejecter:(RCTPromiseRejectBlock)reject)

@end
```

#### Android Native Module (Java)

**CalendarModule.java**
```java
package com.myapp;

import com.facebook.react.bridge.ReactApplicationContext;
import com.facebook.react.bridge.ReactContextBaseJavaModule;
import com.facebook.react.bridge.ReactMethod;
import com.facebook.react.bridge.Promise;
import com.facebook.react.bridge.Callback;
import com.facebook.react.bridge.WritableMap;
import com.facebook.react.bridge.Arguments;
import com.facebook.react.modules.core.DeviceEventManagerModule;

import java.util.HashMap;
import java.util.Map;

public class CalendarModule extends ReactContextBaseJavaModule {
    private ReactApplicationContext reactContext;

    public CalendarModule(ReactApplicationContext context) {
        super(context);
        this.reactContext = context;
    }

    // Module name
    @Override
    public String getName() {
        return "CalendarModule";
    }

    // Export method
    @ReactMethod
    public void createEvent(String name, String location, int date) {
        android.util.Log.d("CalendarModule", "Creating event: " + name);
        
        // Native Android code
        // Access Android APIs, UI, etc.
    }

    // Method with callback
    @ReactMethod
    public void findEvents(Callback callback) {
        WritableMap event = Arguments.createMap();
        event.putString("name", "Meeting");
        event.putString("date", "2024-01-01");
        
        WritableArray events = Arguments.createArray();
        events.pushMap(event);
        
        callback.invoke(null, events); // (error, result)
    }

    // Method with Promise
    @ReactMethod
    public void getEventById(String eventId, Promise promise) {
        if (eventId != null && !eventId.isEmpty()) {
            WritableMap event = Arguments.createMap();
            event.putString("id", eventId);
            event.putString("name", "Birthday Party");
            event.putString("date", "2024-12-25");
            promise.resolve(event);
        } else {
            promise.reject("not_found", "Event not found");
        }
    }

    // Send events to JavaScript
    private void sendEventToJS(String eventName, WritableMap params) {
        reactContext
            .getJSModule(DeviceEventManagerModule.RCTDeviceEventEmitter.class)
            .emit(eventName, params);
    }

    // Export constants
    @Override
    public Map<String, Object> getConstants() {
        final Map<String, Object> constants = new HashMap<>();
        constants.put("DEFAULT_EVENT_COLOR", "blue");
        constants.put("MAX_ATTENDEES", 100);
        return constants;
    }
}
```

**Register Module (MainApplication.java)**
```java
import com.myapp.CalendarModule;

@Override
protected List<ReactPackage> getPackages() {
    return Arrays.<ReactPackage>asList(
        new MainReactPackage(),
        new CalendarPackage() // Custom package
    );
}
```

**CalendarPackage.java**
```java
package com.myapp;

import com.facebook.react.ReactPackage;
import com.facebook.react.bridge.NativeModule;
import com.facebook.react.bridge.ReactApplicationContext;
import com.facebook.react.uimanager.ViewManager;

import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class CalendarPackage implements ReactPackage {
    @Override
    public List<NativeModule> createNativeModules(
            ReactApplicationContext reactContext) {
        List<NativeModule> modules = new ArrayList<>();
        modules.add(new CalendarModule(reactContext));
        return modules;
    }

    @Override
    public List<ViewManager> createViewManagers(
            ReactApplicationContext reactContext) {
        return Collections.emptyList();
    }
}
```

#### Android Native Module (Kotlin)

**CalendarModule.kt**
```kotlin
package com.myapp

import com.facebook.react.bridge.*
import com.facebook.react.modules.core.DeviceEventManagerModule
import android.util.Log

class CalendarModule(reactContext: ReactApplicationContext) :
    ReactContextBaseJavaModule(reactContext) {

    override fun getName(): String {
        return "CalendarModule"
    }

    @ReactMethod
    fun createEvent(name: String, location: String, date: Int) {
        Log.d("CalendarModule", "Creating event: $name")
        
        // Native Kotlin code
        // Access Android APIs
    }

    @ReactMethod
    fun findEvents(callback: Callback) {
        val event = Arguments.createMap().apply {
            putString("name", "Meeting")
            putString("date", "2024-01-01")
        }
        
        val events = Arguments.createArray().apply {
            pushMap(event)
        }
        
        callback.invoke(null, events)
    }

    @ReactMethod
    fun getEventById(eventId: String, promise: Promise) {
        if (eventId.isNotEmpty()) {
            val event = Arguments.createMap().apply {
                putString("id", eventId)
                putString("name", "Birthday Party")
                putString("date", "2024-12-25")
            }
            promise.resolve(event)
        } else {
            promise.reject("not_found", "Event not found")
        }
    }

    private fun sendEventToJS(eventName: String, params: WritableMap) {
        reactApplicationContext
            .getJSModule(DeviceEventManagerModule.RCTDeviceEventEmitter::class.java)
            .emit(eventName, params)
    }

    override fun getConstants(): Map<String, Any> {
        return mapOf(
            "DEFAULT_EVENT_COLOR" to "blue",
            "MAX_ATTENDEES" to 100
        )
    }
}
```

### 3. Using Native Modules in JavaScript

#### Basic Usage

```javascript
// Import native module
import { NativeModules, NativeEventEmitter, Platform } from 'react-native';

const { CalendarModule } = NativeModules;

// Access constants
console.log(CalendarModule.DEFAULT_EVENT_COLOR); // "blue"
console.log(CalendarModule.MAX_ATTENDEES); // 100

// Call methods
class CalendarManager {
  constructor() {
    this.eventEmitter = new NativeEventEmitter(CalendarModule);
    this.setupListeners();
  }

  // Call native method (fire and forget)
  createEvent(name, location, date) {
    CalendarModule.createEvent(name, location, date);
  }

  // Call with callback
  findEvents(callback) {
    CalendarModule.findEvents((error, events) => {
      if (error) {
        console.error('Error finding events:', error);
      } else {
        callback(events);
      }
    });
  }

  // Call with Promise (recommended)
  async getEventById(eventId) {
    try {
      const event = await CalendarModule.getEventById(eventId);
      return event;
    } catch (error) {
      console.error('Error getting event:', error);
      throw error;
    }
  }

  // Listen to native events
  setupListeners() {
    this.eventEmitter.addListener('EventCreated', (event) => {
      console.log('Event created:', event);
    });

    this.eventEmitter.addListener('EventDeleted', (event) => {
      console.log('Event deleted:', event);
    });
  }

  // Clean up
  removeListeners() {
    this.eventEmitter.removeAllListeners('EventCreated');
    this.eventEmitter.removeAllListeners('EventDeleted');
  }
}

// Usage in component
const App = () => {
  const [events, setEvents] = useState([]);
  const calendarManager = useRef(new CalendarManager()).current;

  useEffect(() => {
    loadEvents();
    return () => calendarManager.removeListeners();
  }, []);

  const loadEvents = async () => {
    try {
      const event = await calendarManager.getEventById('123');
      setEvents([event]);
    } catch (error) {
      console.error(error);
    }
  };

  const handleCreateEvent = () => {
    calendarManager.createEvent('Meeting', 'Office', Date.now());
  };

  return (
    <View>
      <Button title="Create Event" onPress={handleCreateEvent} />
      {events.map(event => (
        <Text key={event.id}>{event.name}</Text>
      ))}
    </View>
  );
};
```

### 4. Native UI Components

#### Creating Custom Native Views

**iOS (Objective-C) - MapView**

**MapViewManager.h**
```objective-c
#import <React/RCTViewManager.h>

@interface MapViewManager : RCTViewManager
@end
```

**MapViewManager.m**
```objective-c
#import "MapViewManager.h"
#import <MapKit/MapKit.h>

@implementation MapViewManager

RCT_EXPORT_MODULE(MapView)

- (UIView *)view
{
  MKMapView *mapView = [[MKMapView alloc] init];
  return mapView;
}

// Export properties
RCT_EXPORT_VIEW_PROPERTY(region, MKCoordinateRegion)
RCT_EXPORT_VIEW_PROPERTY(showsUserLocation, BOOL)
RCT_EXPORT_VIEW_PROPERTY(onRegionChange, RCTBubblingEventBlock)

// Export methods
RCT_EXPORT_METHOD(animateToRegion:(nonnull NSNumber *)reactTag
                  latitude:(double)latitude
                  longitude:(double)longitude)
{
  [self.bridge.uiManager addUIBlock:^(RCTUIManager *uiManager, 
                                      NSDictionary<NSNumber *,UIView *> *viewRegistry) {
    MKMapView *mapView = (MKMapView *)viewRegistry[reactTag];
    if ([mapView isKindOfClass:[MKMapView class]]) {
      MKCoordinateRegion region = MKCoordinateRegionMake(
        CLLocationCoordinate2DMake(latitude, longitude),
        MKCoordinateSpanMake(0.1, 0.1)
      );
      [mapView setRegion:region animated:YES];
    }
  }];
}

@end
```

**Android (Java) - MapView**

**MapViewManager.java**
```java
package com.myapp;

import com.facebook.react.uimanager.SimpleViewManager;
import com.facebook.react.uimanager.ThemedReactContext;
import com.facebook.react.uimanager.annotations.ReactProp;
import com.google.android.gms.maps.MapView;
import com.google.android.gms.maps.model.LatLng;
import com.google.android.gms.maps.CameraUpdateFactory;

public class MapViewManager extends SimpleViewManager<MapView> {

    @Override
    public String getName() {
        return "MapView";
    }

    @Override
    protected MapView createViewInstance(ThemedReactContext reactContext) {
        MapView mapView = new MapView(reactContext);
        mapView.onCreate(null);
        mapView.onResume();
        return mapView;
    }

    @ReactProp(name = "latitude")
    public void setLatitude(MapView view, double latitude) {
        // Store for later use
    }

    @ReactProp(name = "longitude")
    public void setLongitude(MapView view, double longitude) {
        // Store for later use
    }

    @ReactProp(name = "showsUserLocation")
    public void setShowsUserLocation(MapView view, boolean show) {
        view.getMapAsync(googleMap -> {
            googleMap.setMyLocationEnabled(show);
        });
    }
}
```

**Using Custom Native Component**

```javascript
// MapView.js
import { requireNativeComponent, findNodeHandle, UIManager } from 'react-native';
import React, { useRef, useImperativeHandle, forwardRef } from 'react';

const NativeMapView = requireNativeComponent('MapView');

const MapView = forwardRef((props, ref) => {
  const mapRef = useRef(null);

  useImperativeHandle(ref, () => ({
    animateToRegion: (latitude, longitude) => {
      const handle = findNodeHandle(mapRef.current);
      UIManager.dispatchViewManagerCommand(
        handle,
        UIManager.getViewManagerConfig('MapView').Commands.animateToRegion,
        [latitude, longitude]
      );
    }
  }));

  return (
    <NativeMapView
      ref={mapRef}
      {...props}
      onRegionChange={(event) => {
        if (props.onRegionChange) {
          props.onRegionChange(event.nativeEvent);
        }
      }}
    />
  );
});

export default MapView;
```

```javascript
// Usage in App
import MapView from './MapView';

const App = () => {
  const mapRef = useRef(null);

  const handleZoomToLocation = () => {
    mapRef.current?.animateToRegion(37.7749, -122.4194);
  };

  return (
    <View style={{ flex: 1 }}>
      <MapView
        ref={mapRef}
        style={{ flex: 1 }}
        latitude={37.7749}
        longitude={-122.4194}
        showsUserLocation={true}
        onRegionChange={(region) => {
          console.log('Region changed:', region);
        }}
      />
      <Button title="Zoom to San Francisco" onPress={handleZoomToLocation} />
    </View>
  );
};
```

### 5. Bridge Performance Optimization

#### Batching Updates

```javascript
// Bad: Multiple bridge calls
for (let i = 0; i < 100; i++) {
  NativeModules.MyModule.updateItem(i, data[i]);
}

// Good: Single bridge call with batch
NativeModules.MyModule.batchUpdateItems(data);
```

#### Using Native Driver for Animations

```javascript
// Runs on JavaScript thread (60fps difficult)
Animated.timing(animatedValue, {
  toValue: 100,
  duration: 1000,
  useNativeDriver: false // Default
}).start();

// Runs on native thread (smooth 60fps)
Animated.timing(animatedValue, {
  toValue: 100,
  duration: 1000,
  useNativeDriver: true // Recommended for transform, opacity
}).start();
```

#### Avoiding Bridge for UI Updates

```javascript
// Bad: Updating UI via bridge (slow)
setInterval(() => {
  this.setState({ time: new Date().toString() });
}, 16); // 60fps

// Good: Use native animation or RAF
const updateTime = () => {
  requestAnimationFrame(() => {
    // Update without bridge
    updateTime();
  });
};
```

### 6. JSI (JavaScript Interface) - New Architecture

**Direct Synchronous Access to Native**

```javascript
// Old Bridge (Async)
const result = await NativeModules.Math.add(2, 3);

// New JSI (Sync)
const result = global.nativeMath.add(2, 3); // Instant!
```

**Benefits:**
- **Synchronous** calls (no async overhead)
- **Direct access** to native memory
- **Type safety** with TypeScript
- **Better performance** (no serialization)

**Example JSI Module (C++)**

```cpp
// MathModule.h
#include <jsi/jsi.h>

namespace facebook {
namespace react {

class MathModule : public facebook::jsi::HostObject {
public:
  facebook::jsi::Value get(
      facebook::jsi::Runtime &runtime,
      const facebook::jsi::PropNameID &name) override {
    
    auto methodName = name.utf8(runtime);
    
    if (methodName == "add") {
      return facebook::jsi::Function::createFromHostFunction(
        runtime,
        name,
        2,
        [](facebook::jsi::Runtime &rt,
           const facebook::jsi::Value &thisValue,
           const facebook::jsi::Value *arguments,
           size_t count) -> facebook::jsi::Value {
          double a = arguments[0].asNumber();
          double b = arguments[1].asNumber();
          return facebook::jsi::Value(a + b);
        }
      );
    }
    
    return facebook::jsi::Value::undefined();
  }
};

} // namespace react
} // namespace facebook
```

### 7. Complete Real-World Example

```javascript
// BiometricAuthModule.js
import { NativeModules, Platform } from 'react-native';

const { BiometricAuth } = NativeModules;

export class BiometricAuthManager {
  // Check if biometric auth is available
  static async isAvailable() {
    try {
      const result = await BiometricAuth.isAvailable();
      return result;
    } catch (error) {
      console.error('Biometric check failed:', error);
      return false;
    }
  }

  // Authenticate user
  static async authenticate(reason) {
    try {
      const result = await BiometricAuth.authenticate({
        reason: reason || 'Authenticate to continue',
        fallbackLabel: 'Use Passcode',
        cancelLabel: 'Cancel'
      });
      return { success: true, ...result };
    } catch (error) {
      return { success: false, error: error.message };
    }
  }

  // Get biometric type
  static async getBiometricType() {
    try {
      const type = await BiometricAuth.getBiometricType();
      return type; // 'FaceID', 'TouchID', 'Fingerprint', etc.
    } catch (error) {
      return null;
    }
  }
}

// Usage in App
const LoginScreen = () => {
  const [authenticated, setAuthenticated] = useState(false);

  useEffect(() => {
    checkBiometricAvailability();
  }, []);

  const checkBiometricAvailability = async () => {
    const available = await BiometricAuthManager.isAvailable();
    if (available) {
      const type = await BiometricAuthManager.getBiometricType();
      console.log(`${type} is available`);
    }
  };

  const handleBiometricLogin = async () => {
    const result = await BiometricAuthManager.authenticate(
      'Log in to your account'
    );
    
    if (result.success) {
      setAuthenticated(true);
      navigation.navigate('Home');
    } else {
      Alert.alert('Authentication Failed', result.error);
    }
  };

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Login</Text>
      <TouchableOpacity 
        style={styles.button} 
        onPress={handleBiometricLogin}
      >
        <Text style={styles.buttonText}>
          Login with {Platform.OS === 'ios' ? 'Face ID' : 'Fingerprint'}
        </Text>
      </TouchableOpacity>
    </View>
  );
};
```

### Summary

**Key Points:**
1. **Bridge Architecture** - Async communication via JSON messages
2. **Native Modules** - Expose native functionality to JavaScript
3. **Native Components** - Create custom UI components
4. **Event Emitters** - Native-to-JS event communication
5. **Performance** - Batch updates, use native driver
6. **JSI** - New synchronous architecture
7. **Platform-Specific** - Handle iOS and Android differences

JavaScript interacts with native mobile components through a sophisticated bridge system that enables web developers to access the full power of native platforms while writing primarily JavaScript code.
```


```

----

