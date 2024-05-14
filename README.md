From: https://github.com/MagicalMadoka

### 油猴脚本
```js
// ==UserScript==
// @name ChatGPT Backend API Hook
// @namespace http://tampermonkey.net/
// @version 0.5
// @description Hook ChatGPT backend API and add missing features
// @match https://chatgpt.com/*
// @grant none
// ==/UserScript==

(function() {
   'use strict';


    const mockResponse = `{
    "models": [
        {
            "slug": "text-davinci-002-render-sha",
            "max_tokens": 8191,
            "title": "Default (GPT-3.5)",
            "description": "我们最快的模型，非常适合大多数日常任务。",
            "tags": [
                "gpt3.5"
            ],
            "capabilities": {},
            "product_features": {}
        },
        {
            "slug": "gpt-4o",
            "max_tokens": 8192,
            "title": "Scallion",
            "description": "浏览、高级数据分析和 DALL·E 现已集成到 GPT-4 中",
            "tags": [
                "confidential",
                "gpt4"
            ],
            "capabilities": {},
            "product_features": {
                "attachments": {
                    "type": "retrieval",
                    "accepted_mime_types": [
                        "text/x-java",
                        "application/x-latext",
                        "text/javascript",
                        "text/x-script.python",
                        "application/pdf",
                        "text/html",
                        "text/x-php",
                        "text/x-c",
                        "text/x-csharp",
                        "application/vnd.openxmlformats-officedocument.presentationml.presentation",
                        "text/x-tex",
                        "application/json",
                        "text/plain",
                        "application/msword",
                        "text/x-ruby",
                        "text/markdown",
                        "text/x-sh",
                        "text/x-typescript",
                        "text/x-c++",
                        "application/vnd.openxmlformats-officedocument.wordprocessingml.document"
                    ],
                    "image_mime_types": [
                        "image/jpeg",
                        "image/gif",
                        "image/webp",
                        "image/png"
                    ],
                    "can_accept_all_mime_types": true
                }
            },
            "enabled_tools": [
                "tools",
                "tools2"
            ]
        },
        {
            "slug": "auto",
            "max_tokens": 8192,
            "title": "Dynamic",
            "description": "使用合适的模型来满足我的请求",
            "tags": [
                "confidential",
                "gpt4"
            ],
            "capabilities": {},
            "product_features": {
                "attachments": {
                    "type": "retrieval",
                    "accepted_mime_types": [
                        "text/x-java",
                        "application/x-latext",
                        "text/javascript",
                        "text/x-script.python",
                        "application/pdf",
                        "text/html",
                        "text/x-php",
                        "text/x-c",
                        "text/x-csharp",
                        "application/vnd.openxmlformats-officedocument.presentationml.presentation",
                        "text/x-tex",
                        "application/json",
                        "text/plain",
                        "application/msword",
                        "text/x-ruby",
                        "text/markdown",
                        "text/x-sh",
                        "text/x-typescript",
                        "text/x-c++",
                        "application/vnd.openxmlformats-officedocument.wordprocessingml.document"
                    ],
                    "image_mime_types": [
                        "image/jpeg",
                        "image/gif",
                        "image/webp",
                        "image/png"
                    ],
                    "can_accept_all_mime_types": true
                }
            },
            "enabled_tools": [
                "tools",
                "tools2"
            ]
        }
    ],
    "categories": [
        {
            "category": "gpt_3.5",
            "human_category_name": "GPT-3.5",
            "human_category_short_name": "3.5",
            "icon": "bolt",
            "icon_src": "data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggZmlsbC1ydWxlPSJldmVub2RkIiBjbGlwLXJ1bGU9ImV2ZW5vZGQiIGQ9Ik0xMi41NjU1IDIuMTEwN0MxMy41Njg2IDAuOTIxNiAxNS40OTU2IDEuODU3NjEgMTUuMTgxIDMuMzgxMjJMMTQuMjI3NCA4LjAwMDAzSDE5LjkyMzlDMjEuMTk5OSA4LjAwMDAzIDIxLjg5MzIgOS40OTE5NyAyMS4wNzA0IDEwLjQ2NzNMMTEuNDM0MyAyMS44ODk0QzEwLjQzMTEgMjMuMDc4NSA4LjUwNDI0IDIyLjE0MjUgOC44MTg3OSAyMC42MTg5TDkuNzcyMzYgMTZINC4wNzU4OEMyLjc5OTg3IDE2IDIuMTA2NTggMTQuNTA4MSAyLjkyOTM4IDEzLjUzMjhMMTIuNTY1NSAyLjExMDdaIiBmaWxsPSIjMjgyODI4Ii8+Cjwvc3ZnPgo=",
            "subscription_level": "free",
            "default_model": "text-davinci-002-render-sha",
            "code_interpreter_model": "text-davinci-002-render-sha-code-interpreter",
            "plugins_model": "text-davinci-002-render-sha-plugins",
            "color": "#47C761",
            "short_explainer": "非常适合用于日常任务",
            "tagline": "最快速"
        },
        {
            "category": "AG8PqS2q",
            "human_category_name": "GPT-4o",
            "human_category_short_name": "4o",
            "icon": "stars",
            "icon_src": "data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggZD0iTTE5LjkxOTQgMC44OTY4ODhDMTkuODkzOCAwLjY3MDk5NCAxOS43MDI4IDAuNTAwMjMgMTkuNDc1NSAwLjVDMTkuMjQ4MSAwLjQ5OTc3IDE5LjA1NjcgMC42NzAxMzEgMTkuMDMwOCAwLjg5NTk4QzE4LjkwOTQgMS45NDc0IDE4LjU5NzIgMi42Njg3MiAxOC4xMDggMy4xNTc5NkMxNy42MTg3IDMuNjQ3MjEgMTYuODk3NCAzLjk1OTQ1IDE1Ljg0NTkgNC4wODA3MkMxNS42MjAxIDQuMTA2NzcgMTUuNDQ5OCA0LjI5ODEyIDE1LjQ1IDQuNTI1NDZDMTUuNDUwMiA0Ljc1MjggMTUuNjIxIDQuOTQzOCAxNS44NDY5IDQuOTY5MzhDMTYuODgwNSA1LjA4NjQ2IDE3LjYxODMgNS4zOTg2NCAxOC4xMiA1Ljg5MTI1QzE4LjYxODkgNi4zODExOCAxOC45MzcgNy4xMDE0NyAxOS4wMjk1IDguMTQyMzVDMTkuMDUwMSA4LjM3MzI5IDE5LjI0MzYgOC41NTAyNiAxOS40NzU1IDguNTVDMTkuNzA3MyA4LjU0OTc0IDE5LjkwMDYgOC4zNzIzNCAxOS45MjA1IDguMTQxMzVDMjAuMDA5MiA3LjExODA1IDIwLjMyNyA2LjM4MTU0IDIwLjgyOTIgNS44NzkyOUMyMS4zMzE2IDUuMzc3MDUgMjIuMDY4IDUuMDU5MTMgMjMuMDkxMyA0Ljk3MDU2QzIzLjMyMjMgNC45NTA1NiAyMy40OTk4IDQuNzU3MzYgMjMuNSA0LjUyNTUxQzIzLjUwMDIgNC4yOTM2NSAyMy4zMjMyIDQuMTAwMDUgMjMuMDkyMyA0LjA3OTU0QzIyLjA1MTUgMy45ODcwOCAyMS4zMzEyIDMuNjY4OTEgMjAuODQxMiAzLjE2OTk2QzIwLjM0ODcgMi42NjgyNyAyMC4wMzY0IDEuOTMwNTMgMTkuOTE5NCAwLjg5Njg4OFoiIGZpbGw9IiMyODI4MjgiLz4KPHBhdGggZD0iTTExLjk5MjYgMy44MjA1N0MxMS45MjY5IDMuMjM5NjkgMTEuNDM1OCAyLjgwMDYgMTAuODUxMiAyLjhDMTAuMjY2NiAyLjc5OTQgOS43NzQ1MiAzLjIzNzQ4IDkuNzA3NTkgMy44MTgyM0M5LjM5NTczIDYuNTIxOTEgOC41OTI4MyA4LjM3NjY4IDcuMzM0NzYgOS42MzQ3NkM2LjA3NjcgMTAuODkyOCA0LjIyMTkxIDExLjY5NTcgMS41MTgyMyAxMi4wMDc2QzAuOTM3NDg0IDEyLjA3NDUgMC40OTk0MDMgMTIuNTY2NiAwLjUwMDAwMSAxMy4xNTEyQzAuNTAwNTk5IDEzLjczNTggMC45Mzk2OTIgMTQuMjI2OSAxLjUyMDU3IDE0LjI5MjZDNC4xNzg1MiAxNC41OTM3IDYuMDc1NTUgMTUuMzk2NSA3LjM2NTU5IDE2LjY2MzNDOC42NDg2MiAxNy45MjMxIDkuNDY2NzYgMTkuNzc1MSA5LjcwNDQ4IDIyLjQ1MThDOS43NTcyNyAyMy4wNDU2IDEwLjI1NTEgMjMuNTAwNyAxMC44NTEzIDIzLjVDMTEuNDQ3NSAyMy40OTkzIDExLjk0NDMgMjMuMDQzMSAxMS45OTU3IDIyLjQ0OTFDMTIuMjIzNCAxOS44MTc4IDEzLjA0MSAxNy45MjQgMTQuMzMyNCAxNi42MzI0QzE1LjYyNCAxNS4zNDEgMTcuNTE3OCAxNC41MjM0IDIwLjE0OTEgMTQuMjk1N0MyMC43NDMxIDE0LjI0NDMgMjEuMTk5MyAxMy43NDc1IDIxLjIgMTMuMTUxM0MyMS4yMDA3IDEyLjU1NTEgMjAuNzQ1NiAxMi4wNTczIDIwLjE1MTggMTIuMDA0NUMxNy40NzUxIDExLjc2NjggMTUuNjIzMSAxMC45NDg3IDE0LjM2MzMgOS42NjU1OUMxMy4wOTY1IDguMzc1NTUgMTIuMjkzNyA2LjQ3ODUyIDExLjk5MjYgMy44MjA1N1oiIGZpbGw9IiMyODI4MjgiLz4KPC9zdmc+Cg==",
            "subscription_level": "plus",
            "default_model": "gpt-4o",
            "color": "#5B41F9",
            "short_explainer": "Newest and most advanced model",
            "tagline": "智能且快速"
        },
        {
            "category": "auto",
            "human_category_name": "Dynamic",
            "human_category_short_name": "",
            "icon": "connected",
            "icon_src": "data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgZmlsbD0ibm9uZSIgdmlld0JveD0iMCAwIDI0IDI0Ij48cGF0aCBmaWxsPSJjdXJyZW50Q29sb3IiIGZpbGwtcnVsZT0iZXZlbm9kZCIgZD0iTTEyIDcuNDJhMjIgMjIgMCAwIDAtMi40NTMgMi4xMjdBMjIgMjIgMCAwIDAgNy40MiAxMmEyMiAyMiAwIDAgMCAyLjEyNyAyLjQ1M2MuODA3LjgwOCAxLjYzNiAxLjUyIDIuNDUzIDIuMTI4YTIyIDIyIDAgMCAwIDIuNDUzLTIuMTI4QTIyIDIyIDAgMCAwIDE2LjU4IDEyYTIyIDIyIDAgMCAwLTIuMTI3LTIuNDUzQTIyIDIyIDAgMCAwIDEyIDcuNDJtMS43NTEtMS4xNTRhMjUgMjUgMCAwIDEgMi4xMDQgMS44OCAyNSAyNSAwIDAgMSAxLjg4IDIuMTAzYy4zMTYtLjU1LjU3Ni0xLjA4NS43NzktMS41OS4zNS0uODc4LjUwNy0xLjYyNS41MDMtMi4yMDYtLjAwMy0uNTc0LS4xNi0uOTEzLS4zNTgtMS4xMTEtLjE5OS0uMTk5LS41MzctLjM1Ni0xLjExMi0uMzYtLjU4LS4wMDMtMS4zMjguMTUzLTIuMjA1LjUwNC0uNTA2LjIwMy0xLjA0LjQ2NC0xLjU5Ljc4Wm0zLjk4MyA3LjQ4NWEyNSAyNSAwIDAgMS0xLjg4IDIuMTA0IDI1IDI1IDAgMCAxLTIuMTAzIDEuODggMTMgMTMgMCAwIDAgMS41OS43NzljLjg3OC4zNSAxLjYyNS41MDcgMi4yMDYuNTAzLjU3NC0uMDAzLjkxMy0uMTYgMS4xMTEtLjM1OC4xOTktLjE5OS4zNTYtLjUzOC4zNi0xLjExMi4wMDMtLjU4LS4xNTQtMS4zMjgtLjUwNC0yLjIwNWExMyAxMyAwIDAgMC0uNzgtMS41OVpNMTIgMTguOTljLjg5LjU3IDEuNzY4IDEuMDMgMi42MDUgMS4zNjQgMS4wMjYuNDEgMi4wMzYuNjUyIDIuOTU1LjY0Ni45MjUtLjAwNiAxLjgyOC0uMjY3IDIuNS0uOTQuNjczLS42NzIuOTM0LTEuNTc1Ljk0LTIuNS4wMDYtLjkxOS0uMjM2LTEuOTI5LS42NDYtMi45NTRBMTUuNyAxNS43IDAgMCAwIDE4Ljk5IDEyYTE1LjYgMTUuNiAwIDAgMCAxLjM2NC0yLjYwNmMuNDEtMS4wMjUuNjUyLTIuMDM1LjY0Ni0yLjk1NC0uMDA2LS45MjUtLjI2Ny0xLjgyOC0uOTQtMi41LS42NzItLjY3My0xLjU3NS0uOTM0LTIuNS0uOTQtLjkxOS0uMDA2LTEuOTI5LjIzNS0yLjk1NC42NDYtLjgzOC4zMzUtMS43MTYuNzk1LTIuNjA2IDEuMzY0YTE1LjcgMTUuNyAwIDAgMC0yLjYwNi0xLjM2NEM4LjM3IDMuMjM2IDcuMzYgMi45OTQgNi40NCAzYy0uOTI1LjAwNi0xLjgyOC4yNjctMi41Ljk0LS42NzMuNjcyLS45MzQgMS41NzUtLjk0IDIuNS0uMDA2LjkxOS4yMzUgMS45MjkuNjQ2IDIuOTU1QTE1LjcgMTUuNyAwIDAgMCA1LjAxIDEyYy0uNTcuODktMS4wMyAxLjc2OC0xLjM2NCAyLjYwNS0uNDEgMS4wMjYtLjY1MiAyLjAzNi0uNjQ2IDIuOTU1LjAwNi45MjUuMjY3IDEuODI4Ljk0IDIuNS42NzIuNjczIDEuNTc1LjkzNCAyLjUuOTQuOTIuMDA2IDEuOTMtLjIzNSAyLjk1NS0uNjQ2QTE1LjcgMTUuNyAwIDAgMCAxMiAxOC45OW0tMS43NTEtMS4yNTVhMjUgMjUgMCAwIDEtMi4xMDQtMS44OCAyNSAyNSAwIDAgMS0xLjg4LTIuMTA0Yy0uMzE1LjU1LS41NzYgMS4wODUtLjc3OSAxLjU5LS4zNS44NzgtLjUwNyAxLjYyNS0uNTAzIDIuMjA2LjAwMy41NzQuMTYuOTEzLjM1OSAxLjExMS4xOTguMTk5LjUzNy4zNTYgMS4xMTEuMzYuNTguMDAzIDEuMzI4LS4xNTMgMi4yMDUtLjUwNC41MDYtLjIwMyAxLjA0LS40NjMgMS41OS0uNzhabS0zLjk4My03LjQ4NmEyNSAyNSAwIDAgMSAxLjg4LTIuMTA0IDI1IDI1IDAgMCAxIDIuMTAzLTEuODggMTMgMTMgMCAwIDAtMS41OS0uNzc5Yy0uODc4LS4zNS0xLjYyNS0uNTA3LTIuMjA2LS41MDMtLjU3NC4wMDMtLjkxMy4xNi0xLjExMS4zNTktLjE5OS4xOTgtLjM1Ni41MzctLjM2IDEuMTExLS4wMDMuNTguMTUzIDEuMzI4LjUwNCAyLjIwNS4yMDMuNTA2LjQ2NCAxLjA0Ljc4IDEuNTlaIiBjbGlwLXJ1bGU9ImV2ZW5vZGQiPjwvcGF0aD48L3N2Zz4=",
            "subscription_level": "free",
            "default_model": "auto",
            "plugins_model": "gpt-4-plugins",
            "color": "",
            "short_explainer": "为改善速度和智能程度而进行了优化。",
            "tagline": ""
        }
    ]
}`;

const originalFetch = window.fetch;

window.fetch = async function(url, options) {
    if (typeof url === 'string' && url.includes('/backend-api/models')) {
        return new Promise(resolve => {
            resolve(new Response(mockResponse, {
                status: 200,
                headers: { 'Content-Type': 'application/json' }
            }));
        });
    } else {
        return originalFetch(url, options);
    }
};
})();
```
