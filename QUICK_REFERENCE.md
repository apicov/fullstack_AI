# 🚀 Fullstack AI Quick Reference

## 📖 Daily Learning Checklist

### **Morning Routine (5 minutes)**
- [ ] Review yesterday's code
- [ ] Check today's goals in [Dashboard](LEARNING_DASHBOARD.html)
- [ ] Set up workspace (4 browser tabs + IDE)

### **Learning Session (2.5 hours)**
- [ ] **30 min JavaScript** + practice
- [ ] **30 min React** + components  
- [ ] **30 min TinyML** + models
- [ ] **30 min LLMs** + prompts
- [ ] **30 min Integration** project

### **Evening Wrap-up (10 minutes)**
- [ ] Update progress dashboard
- [ ] Write 3 key learnings
- [ ] Plan tomorrow's focus

---

## ⚡ Essential Commands

### **JavaScript Quick Commands**
```javascript
// Modern variable declaration
const immutable = "never changes";
let mutable = "can change";

// Arrow functions
const add = (a, b) => a + b;

// Async/await
const fetchData = async () => {
  const response = await fetch('/api/data');
  return response.json();
};

// Destructuring
const { name, age } = user;
const [first, second] = array;

// Array methods
data.map(item => item.name)
    .filter(name => name.length > 3)
    .forEach(name => console.log(name));
```

### **React Quick Commands**
```jsx
// Functional component with hooks
import React, { useState, useEffect } from 'react';

function MyComponent() {
  const [count, setCount] = useState(0);
  
  useEffect(() => {
    // Side effects here
  }, [count]);

  return (
    <div onClick={() => setCount(count + 1)}>
      Count: {count}
    </div>
  );
}

// Props and children
function Parent() {
  return (
    <Child name="value" onAction={handleAction}>
      <p>Child content</p>
    </Child>
  );
}
```

### **TinyML Quick Commands**
```javascript
// Load TensorFlow.js
import * as tf from '@tensorflow/tfjs';

// Create simple model
const model = tf.sequential({
  layers: [
    tf.layers.dense({inputShape: [4], units: 10, activation: 'relu'}),
    tf.layers.dense({units: 1, activation: 'sigmoid'})
  ]
});

// Compile and train
model.compile({optimizer: 'adam', loss: 'binaryCrossentropy'});
await model.fit(xs, ys, {epochs: 100});

// Make prediction
const prediction = model.predict(tf.tensor2d([[1, 2, 3, 4]]));
```

### **LLM Quick Commands**
```javascript
// OpenAI API call
const response = await fetch('https://api.openai.com/v1/chat/completions', {
  method: 'POST',
  headers: {
    'Authorization': `Bearer ${apiKey}`,
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    model: 'gpt-3.5-turbo',
    messages: [
      {role: 'system', content: 'You are a helpful assistant.'},
      {role: 'user', content: prompt}
    ]
  })
});

// Process response
const data = await response.json();
const answer = data.choices[0].message.content;
```

---

## 🔧 Setup Commands

### **Project Initialization**
```bash
# Create new project
mkdir my-ai-project && cd my-ai-project

# Initialize JavaScript project
npm init -y
npm install express cors dotenv

# Create React app
npx create-react-app frontend
cd frontend && npm install axios @tensorflow/tfjs

# Install TinyML dependencies
npm install @tensorflow/tfjs-node
pip install tensorflow keras numpy

# Environment setup
echo "OPENAI_API_KEY=your-key-here" > .env
```

### **Development Workflow**
```bash
# Start all services
npm run dev          # Backend
npm start           # React (in frontend/)
python server.py    # AI services

# Common debugging
npm run build       # Build React for production
npm test           # Run tests
git add . && git commit -m "Weekly project complete"
```

---

## 🐛 Quick Troubleshooting

### **JavaScript Issues**
| Problem | Solution |
|---------|----------|
| `undefined is not a function` | Check if function exists, use `?.` operator |
| `Promise rejected` | Add `.catch()` or `try/catch` with async/await |
| `CORS error` | Add CORS middleware to backend |
| `Module not found` | Check import paths, run `npm install` |

### **React Issues**
| Problem | Solution |
|---------|----------|
| Component not updating | Check state mutations, use `setState` properly |
| `Cannot read property` | Add conditional rendering: `{data && data.map(...)}` |
| Infinite re-renders | Check `useEffect` dependencies |
| Styles not applying | Import CSS file, check className spelling |

### **TinyML Issues**
| Problem | Solution |
|---------|----------|
| Model not loading | Check model path, ensure TensorFlow.js is loaded |
| Slow inference | Use smaller model, optimize input preprocessing |
| Memory errors | Dispose tensors: `tensor.dispose()` |
| NaN predictions | Check input data range and preprocessing |

### **LLM Issues**
| Problem | Solution |
|---------|----------|
| API key error | Check environment variables, API key validity |
| Rate limiting | Add delays between requests, implement retry logic |
| Poor responses | Improve prompts, add context, adjust temperature |
| High costs | Set max_tokens, use cheaper models for development |

---

## 📊 Integration Patterns

### **JavaScript ↔ React**
```javascript
// Backend API
app.get('/api/data', (req, res) => {
  res.json({ message: "Hello from backend!" });
});

// React consumption
const [data, setData] = useState(null);
useEffect(() => {
  fetch('/api/data')
    .then(res => res.json())
    .then(setData);
}, []);
```

### **React ↔ TinyML**
```jsx
function AIComponent() {
  const [model, setModel] = useState(null);
  const [prediction, setPrediction] = useState(null);

  useEffect(() => {
    tf.loadLayersModel('/models/my-model.json')
      .then(setModel);
  }, []);

  const predict = (inputData) => {
    if (model) {
      const result = model.predict(tf.tensor2d([inputData]));
      setPrediction(result.dataSync()[0]);
    }
  };
}
```

### **All Technologies Integration**
```javascript
// Complete integration example
class FullStackAI {
  constructor() {
    this.model = null;      // TinyML
    this.llm = new LLMService();  // LLM
    this.server = express();      // JavaScript backend
  }

  async initialize() {
    // Load AI models
    this.model = await tf.loadLayersModel('/models/classifier.json');
    
    // Setup API routes
    this.server.get('/predict', this.handlePrediction.bind(this));
    this.server.post('/chat', this.handleChat.bind(this));
  }

  async handlePrediction(req, res) {
    const prediction = this.model.predict(tf.tensor2d([req.body.data]));
    const explanation = await this.llm.explain(prediction);
    res.json({ prediction, explanation });
  }
}
```

---

## 🎯 Weekly Project Templates

### **Week 1: Hello World**
```
📁 week1-project/
├── 📄 index.html         # Entry point
├── 🔧 script.js          # JavaScript logic
├── ⚛️ App.jsx           # React component
├── 🧠 model.js          # TinyML demo
└── 🤖 llm-demo.js       # LLM integration
```

### **Week 5: IoT Camera**
```
📁 week5-camera/
├── 🍓 raspberry-pi/      # Pi server code
├── ⚛️ react-frontend/    # Video interface
├── 👁️ yolo-detection/    # Browser AI
└── 🗣️ voice-control/     # LLM commands
```

### **Week 12: Capstone**
```
📁 week12-capstone/
├── 🌐 backend/           # Full API server
├── ⚛️ frontend/          # Complete React app
├── 🤖 ai-services/       # All AI models
├── 📱 mobile/            # Optional mobile app
└── ☁️ deployment/        # Production config
```

---

## 📚 Learning Resources

### **Documentation Links**
- **JavaScript**: [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
- **React**: [React Documentation](https://react.dev/)
- **TensorFlow.js**: [TensorFlow.js Guide](https://www.tensorflow.org/js)
- **OpenAI**: [API Documentation](https://platform.openai.com/docs)

### **Quick Tutorials**
- **30-second JS**: Quick concept explanations
- **React in 5 minutes**: Component patterns
- **TinyML basics**: Model deployment
- **Prompt engineering**: LLM best practices

### **Community Help**
- **Stack Overflow**: Tag your questions properly
- **Discord**: Real-time help from peers
- **GitHub Issues**: Report bugs and get help
- **Office Hours**: Weekly live Q&A sessions

---

## 🎉 Success Metrics

### **Daily Wins**
- [ ] Completed 4 technology sessions
- [ ] Built something that works
- [ ] Made cross-technology connections
- [ ] Updated progress dashboard

### **Weekly Achievements**
- [ ] Finished weekly project
- [ ] Integrated multiple technologies
- [ ] Solved at least one challenging bug
- [ ] Helped another learner

### **Monthly Milestones**
- [ ] Built production-ready application
- [ ] Demonstrated all learned skills
- [ ] Contributed to community
- [ ] Planned next learning goals

---

## 🚀 Next Steps

### **Stuck? Try This Order:**
1. **Check this reference** for quick solutions
2. **Search course Discord** for similar issues
3. **Google the exact error** message
4. **Ask in community** with code sample
5. **Join office hours** for live help

### **Feeling Confident? Level Up:**
1. **Add new features** to weekly projects
2. **Help other learners** in Discord
3. **Share your project** on social media
4. **Start planning** your capstone project

**Remember: Every expert was once a beginner. Keep building!** 🌟

---

*Bookmark this page for instant access to everything you need!* 📖✨ 