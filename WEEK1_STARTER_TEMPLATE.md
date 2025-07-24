# Week 1 Starter Template: Multi-Tech Hello World

## 🎯 Project Overview

Build your first project that uses all four technologies:
- **JavaScript**: Console app with async operations
- **React**: Simple component with state  
- **TinyML**: Basic model that runs in browser
- **LLM**: Simple text generation

## 📁 Project Structure

```
week1-hello-world/
├── javascript/
│   ├── hello-world.js
│   └── async-demo.js
├── react/
│   ├── src/
│   │   ├── HelloWorld.js
│   │   └── App.js
│   └── package.json
├── tinyml/
│   ├── simple-model.html
│   └── model-demo.js
├── llm/
│   ├── text-generation.js
│   └── prompt-examples.md
└── README.md
```

## 💻 Code Templates

### 1. JavaScript Hello World with Async

**File: `javascript/hello-world.js`**
```javascript
// Modern JavaScript with async/await
class HelloWorldApp {
    constructor() {
        this.message = "Hello from JavaScript!";
        this.data = [];
    }

    // Async function to simulate API call
    async fetchData() {
        console.log("Fetching data...");
        
        // Simulate network delay
        await this.delay(1000);
        
        const sampleData = [
            { id: 1, name: "JavaScript", type: "Language" },
            { id: 2, name: "React", type: "Framework" },
            { id: 3, name: "TinyML", type: "Edge AI" },
            { id: 4, name: "LLM", type: "AI Model" }
        ];
        
        this.data = sampleData;
        console.log("Data fetched:", this.data);
        return this.data;
    }

    // Utility function for delays
    delay(ms) {
        return new Promise(resolve => setTimeout(resolve, ms));
    }

    // Process data with modern JavaScript features
    processData() {
        // Destructuring and array methods
        const { data } = this;
        
        // Filter and map
        const aiTech = data
            .filter(item => item.type.includes("AI"))
            .map(({ name, type }) => `${name} (${type})`);
        
        console.log("AI Technologies:", aiTech);
        return aiTech;
    }

    // Main application logic
    async run() {
        console.log(this.message);
        
        try {
            await this.fetchData();
            const processed = this.processData();
            
            console.log("🎉 JavaScript Hello World Complete!");
            console.log("Next: Build React component!");
            
        } catch (error) {
            console.error("Error:", error);
        }
    }
}

// Run the application
const app = new HelloWorldApp();
app.run();
```

### 2. React Hello World Component

**File: `react/src/HelloWorld.js`**
```jsx
import React, { useState, useEffect } from 'react';

function HelloWorld() {
    // State management with hooks
    const [message, setMessage] = useState("Hello from React!");
    const [counter, setCounter] = useState(0);
    const [technologies, setTechnologies] = useState([]);
    const [loading, setLoading] = useState(true);

    // Effect hook for data fetching
    useEffect(() => {
        const fetchTechnologies = async () => {
            setLoading(true);
            
            // Simulate API call
            await new Promise(resolve => setTimeout(resolve, 1000));
            
            const techStack = [
                { name: "JavaScript", learned: true, confidence: 7 },
                { name: "React", learned: false, confidence: 3 },
                { name: "TinyML", learned: false, confidence: 2 },
                { name: "LLMs", learned: false, confidence: 1 }
            ];
            
            setTechnologies(techStack);
            setLoading(false);
        };

        fetchTechnologies();
    }, []);

    // Event handlers
    const handleIncrement = () => {
        setCounter(prev => prev + 1);
    };

    const handleTechToggle = (index) => {
        setTechnologies(prev => 
            prev.map((tech, i) => 
                i === index 
                    ? { ...tech, learned: !tech.learned }
                    : tech
            )
        );
    };

    // Render component
    return (
        <div style={styles.container}>
            <header style={styles.header}>
                <h1>{message}</h1>
                <p>Building my first multi-tech project!</p>
            </header>

            <section style={styles.section}>
                <h2>Progress Counter</h2>
                <div style={styles.counter}>
                    <span style={styles.counterText}>{counter}</span>
                    <button 
                        onClick={handleIncrement}
                        style={styles.button}
                    >
                        Add Progress Point
                    </button>
                </div>
            </section>

            <section style={styles.section}>
                <h2>Technology Stack</h2>
                {loading ? (
                    <p>Loading technologies...</p>
                ) : (
                    <div style={styles.techGrid}>
                        {technologies.map((tech, index) => (
                            <div 
                                key={tech.name}
                                style={{
                                    ...styles.techCard,
                                    backgroundColor: tech.learned ? '#e8f5e8' : '#f5f5f5'
                                }}
                                onClick={() => handleTechToggle(index)}
                            >
                                <h3>{tech.name}</h3>
                                <p>Confidence: {tech.confidence}/10</p>
                                <span style={styles.status}>
                                    {tech.learned ? '✅ Learning' : '⭕ To Learn'}
                                </span>
                            </div>
                        ))}
                    </div>
                )}
            </section>

            <footer style={styles.footer}>
                <p>🎯 Next: Add TinyML model!</p>
            </footer>
        </div>
    );
}

// Styles object
const styles = {
    container: {
        maxWidth: '800px',
        margin: '0 auto',
        padding: '20px',
        fontFamily: 'Arial, sans-serif'
    },
    header: {
        textAlign: 'center',
        marginBottom: '30px',
        color: '#333'
    },
    section: {
        marginBottom: '30px',
        padding: '20px',
        border: '1px solid #ddd',
        borderRadius: '8px'
    },
    counter: {
        display: 'flex',
        alignItems: 'center',
        gap: '20px',
        justifyContent: 'center'
    },
    counterText: {
        fontSize: '2em',
        fontWeight: 'bold',
        color: '#007bff'
    },
    button: {
        padding: '10px 20px',
        backgroundColor: '#007bff',
        color: 'white',
        border: 'none',
        borderRadius: '5px',
        cursor: 'pointer',
        fontSize: '16px'
    },
    techGrid: {
        display: 'grid',
        gridTemplateColumns: 'repeat(auto-fit, minmax(180px, 1fr))',
        gap: '15px'
    },
    techCard: {
        padding: '15px',
        border: '1px solid #ccc',
        borderRadius: '8px',
        cursor: 'pointer',
        textAlign: 'center',
        transition: 'transform 0.2s'
    },
    status: {
        fontSize: '14px',
        fontWeight: 'bold'
    },
    footer: {
        textAlign: 'center',
        color: '#666',
        marginTop: '30px'
    }
};

export default HelloWorld;
```

### 3. TinyML in Browser

**File: `tinyml/simple-model.html`**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TinyML Hello World</title>
    <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@latest/dist/tf.min.js"></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
        }
        .container {
            background: rgba(255, 255, 255, 0.1);
            padding: 30px;
            border-radius: 15px;
            backdrop-filter: blur(10px);
        }
        .section {
            margin: 20px 0;
            padding: 20px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
        }
        button {
            background: #28a745;
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 16px;
            margin: 10px 5px;
        }
        button:hover {
            background: #218838;
        }
        .prediction {
            font-size: 18px;
            font-weight: bold;
            color: #ffd700;
        }
        .model-info {
            background: rgba(0, 0, 0, 0.2);
            padding: 15px;
            border-radius: 8px;
            margin: 10px 0;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>🧠 TinyML Hello World</h1>
        <p>Simple machine learning model running in your browser!</p>

        <div class="section">
            <h2>Model Information</h2>
            <div id="modelInfo" class="model-info">
                Loading TensorFlow.js...
            </div>
        </div>

        <div class="section">
            <h2>Simple Number Predictor</h2>
            <p>This model learns to predict: y = 2x + 1</p>
            
            <button onclick="trainModel()">Train Model</button>
            <button onclick="makePrediction()">Make Prediction</button>
            
            <div id="trainingStatus"></div>
            <div id="predictionResult" class="prediction"></div>
        </div>

        <div class="section">
            <h2>Model Architecture</h2>
            <div id="modelSummary"></div>
        </div>
    </div>

    <script>
        let model = null;
        let isTraining = false;

        // Initialize when page loads
        window.onload = async function() {
            await initializeTensorFlow();
            createSimpleModel();
        };

        async function initializeTensorFlow() {
            const info = document.getElementById('modelInfo');
            info.innerHTML = `
                <strong>TensorFlow.js Version:</strong> ${tf.version.tfjs}<br>
                <strong>Backend:</strong> ${tf.getBackend()}<br>
                <strong>Platform:</strong> ${navigator.platform}<br>
                <strong>Status:</strong> Ready for TinyML! 🚀
            `;
        }

        function createSimpleModel() {
            // Create a simple neural network
            model = tf.sequential({
                layers: [
                    tf.layers.dense({
                        inputShape: [1],
                        units: 10,
                        activation: 'relu',
                        name: 'hidden'
                    }),
                    tf.layers.dense({
                        units: 1,
                        name: 'output'
                    })
                ]
            });

            // Compile the model
            model.compile({
                optimizer: tf.train.adam(0.1),
                loss: 'meanSquaredError',
                metrics: ['mse']
            });

            // Display model summary
            const summary = document.getElementById('modelSummary');
            summary.innerHTML = `
                <strong>Layers:</strong> ${model.layers.length}<br>
                <strong>Parameters:</strong> ${model.countParams()}<br>
                <strong>Input Shape:</strong> [null, 1]<br>
                <strong>Output Shape:</strong> [null, 1]<br>
                <strong>Purpose:</strong> Learn y = 2x + 1 function
            `;

            console.log('Model created successfully!');
        }

        async function trainModel() {
            if (isTraining) return;
            
            isTraining = true;
            const statusDiv = document.getElementById('trainingStatus');
            statusDiv.innerHTML = '<p>🔄 Training model...</p>';

            // Generate training data: y = 2x + 1
            const xs = tf.tensor2d([-1, 0, 1, 2, 3, 4], [6, 1]);
            const ys = tf.tensor2d([-1, 1, 3, 5, 7, 9], [6, 1]);

            try {
                // Train the model
                const history = await model.fit(xs, ys, {
                    epochs: 100,
                    callbacks: {
                        onEpochEnd: (epoch, logs) => {
                            if (epoch % 20 === 0) {
                                statusDiv.innerHTML = `
                                    <p>🔄 Epoch ${epoch}/100</p>
                                    <p>Loss: ${logs.loss.toFixed(4)}</p>
                                `;
                            }
                        }
                    }
                });

                statusDiv.innerHTML = `
                    <p>✅ Training complete!</p>
                    <p>Final Loss: ${history.history.loss[history.history.loss.length - 1].toFixed(4)}</p>
                `;

            } catch (error) {
                statusDiv.innerHTML = `<p>❌ Training failed: ${error.message}</p>`;
            }

            // Clean up tensors
            xs.dispose();
            ys.dispose();
            isTraining = false;
        }

        async function makePrediction() {
            if (!model) {
                alert('Please create and train the model first!');
                return;
            }

            const resultDiv = document.getElementById('predictionResult');
            
            // Test with a new value
            const testValue = Math.random() * 10; // Random number 0-10
            const prediction = model.predict(tf.tensor2d([testValue], [1, 1]));
            const predictionValue = await prediction.data();
            
            const expected = 2 * testValue + 1;
            const error = Math.abs(predictionValue[0] - expected);

            resultDiv.innerHTML = `
                <strong>Input:</strong> ${testValue.toFixed(2)}<br>
                <strong>Predicted:</strong> ${predictionValue[0].toFixed(2)}<br>
                <strong>Expected:</strong> ${expected.toFixed(2)}<br>
                <strong>Error:</strong> ${error.toFixed(4)}<br>
                <strong>Accuracy:</strong> ${(100 - (error/expected)*100).toFixed(1)}%
            `;

            // Clean up
            prediction.dispose();
        }
    </script>
</body>
</html>
```

### 4. LLM Text Generation

**File: `llm/text-generation.js`**
```javascript
// Simple LLM demonstration using OpenAI API
class LLMHelloWorld {
    constructor() {
        this.apiKey = 'your-openai-api-key'; // Replace with your key
        this.model = 'gpt-3.5-turbo';
        this.prompts = this.getExamplePrompts();
    }

    getExamplePrompts() {
        return [
            {
                name: "Learning Assistant",
                prompt: "Explain JavaScript promises in simple terms suitable for a beginner."
            },
            {
                name: "Code Helper",
                prompt: "Write a simple React component that displays a counter with increment button."
            },
            {
                name: "Project Idea Generator",
                prompt: "Suggest 3 beginner-friendly projects that combine JavaScript and AI."
            },
            {
                name: "Study Motivator",
                prompt: "Write an encouraging message for someone learning to code their first AI project."
            }
        ];
    }

    // Simulate LLM response (for demo purposes)
    async simulateResponse(prompt) {
        console.log(`🤖 Processing prompt: "${prompt}"`);
        
        // Simulate thinking time
        await this.delay(1500);
        
        // Return a demo response based on prompt type
        if (prompt.toLowerCase().includes('promise')) {
            return {
                response: `JavaScript Promises are like making a reservation at a restaurant:

📞 **Making the Promise**: You call and ask for a table
⏳ **Pending**: You're waiting to hear back
✅ **Fulfilled**: They confirm your reservation  
❌ **Rejected**: They're fully booked

Here's a simple example:
\`\`\`javascript
const reservation = new Promise((resolve, reject) => {
    // Restaurant checks availability
    setTimeout(() => {
        const available = Math.random() > 0.3;
        if (available) {
            resolve("Table reserved for 7 PM!");
        } else {
            reject("Sorry, we're fully booked.");
        }
    }, 1000);
});

reservation
    .then(message => console.log(message))
    .catch(error => console.log(error));
\`\`\`

This way, your code doesn't have to wait around - it can do other things while the promise resolves!`,
                usage: { prompt_tokens: 50, completion_tokens: 120 }
            };
        }
        
        return {
            response: `This is a simulated response to: "${prompt}"
            
🎯 **Key Points:**
• This demonstrates how LLMs process natural language
• Real implementation would use OpenAI API or local models
• Responses can be customized based on context
• Perfect for building intelligent assistants

💡 **Next Steps:**
1. Get an OpenAI API key for real responses
2. Implement proper error handling
3. Add conversation memory
4. Create specialized prompts for your use case`,
            usage: { prompt_tokens: 30, completion_tokens: 80 }
        };
    }

    // Real API call (requires API key)
    async callLLMAPI(prompt) {
        const response = await fetch('https://api.openai.com/v1/chat/completions', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
                'Authorization': `Bearer ${this.apiKey}`
            },
            body: JSON.stringify({
                model: this.model,
                messages: [
                    {
                        role: 'system',
                        content: 'You are a helpful AI tutor specializing in programming and AI education.'
                    },
                    {
                        role: 'user',
                        content: prompt
                    }
                ],
                max_tokens: 200,
                temperature: 0.7
            })
        });

        if (!response.ok) {
            throw new Error(`API Error: ${response.status}`);
        }

        const data = await response.json();
        return {
            response: data.choices[0].message.content,
            usage: data.usage
        };
    }

    async demonstratePrompts() {
        console.log("🚀 LLM Hello World - Demonstrating Different Prompts\n");
        
        for (const { name, prompt } of this.prompts) {
            console.log(`\n📝 ${name}:`);
            console.log(`Prompt: "${prompt}"`);
            console.log("-".repeat(50));
            
            try {
                const result = await this.simulateResponse(prompt);
                console.log(result.response);
                console.log(`\n📊 Tokens used: ${result.usage.completion_tokens}`);
                
            } catch (error) {
                console.error(`❌ Error: ${error.message}`);
            }
            
            console.log("=".repeat(80));
        }
    }

    // Interactive prompt testing
    async testCustomPrompt(userPrompt) {
        console.log(`\n🎯 Testing Custom Prompt:`);
        console.log(`"${userPrompt}"`);
        console.log("-".repeat(50));
        
        try {
            const result = await this.simulateResponse(userPrompt);
            console.log(result.response);
            return result;
            
        } catch (error) {
            console.error(`❌ Error: ${error.message}`);
            return null;
        }
    }

    delay(ms) {
        return new Promise(resolve => setTimeout(resolve, ms));
    }

    // Main demo function
    async run() {
        console.log("🧠 LLM Hello World Starting...\n");
        
        // Show system info
        console.log("🔧 System Information:");
        console.log(`Model: ${this.model}`);
        console.log(`Available Prompts: ${this.prompts.length}`);
        console.log(`Mode: Simulation (set API key for real responses)`);
        
        // Demonstrate different prompts
        await this.demonstratePrompts();
        
        // Test custom prompt
        await this.testCustomPrompt("How can I connect my React app to a TinyML model?");
        
        console.log("\n🎉 LLM Hello World Complete!");
        console.log("Next: Integrate all technologies into one project!");
    }
}

// Run the demo
const llmDemo = new LLMHelloWorld();
llmDemo.run();

// Export for use in other modules
if (typeof module !== 'undefined' && module.exports) {
    module.exports = LLMHelloWorld;
}
```

## 🔗 Integration Challenge

After building each component separately, your challenge is to **connect them all**:

1. **JavaScript** backend serves data to **React** frontend
2. **React** interface displays **TinyML** model predictions
3. **LLM** generates explanations for the AI predictions
4. All technologies work together in one application!

## 📝 Learning Reflection

After completing this project, ask yourself:

1. **What patterns did I see repeated across technologies?**
2. **How do these technologies complement each other?**
3. **What would I build if I had unlimited time?**
4. **Which technology felt most natural, and which was most challenging?**

## 🎯 Next Steps

Ready for Week 2? You'll build:
- **Smart Data Analyzer** with real-time processing
- **Interactive visualizations** with React
- **Anomaly detection** with TinyML
- **Intelligent insights** with LLMs

**Congratulations on your first multi-tech project!** 🎉 