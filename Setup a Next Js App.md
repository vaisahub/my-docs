
PWA - Progressive Web App

## Install -> npm package next-pwa
##         -> workbox-webpack-plugin   

const withPWA = require('next-pwa')({
    dest: 'public',
    disable: process.env.NODE_ENV === 'development',
    // optionally, you can configure other PWA options here
  });
  
module.exports = withPWA({
    // Your existing Next.js configuration
    reactStrictMode: true,
    // Other configurations...
});

## Configure: es lint

--> npm install --save-dev eslint eslint-config-next eslint-plugin-react eslint-plugin-import husky lint-staged
--> .eslintignore
--> 

"scripts": {
  "dev": "next dev",
  "build": "next build",
  "start": "next start",
  "lint": "eslint . --ext .js,.jsx,.ts,.tsx", // Lint all files
  "lint:fix": "eslint . --ext .js,.jsx,.ts,.tsx --fix" // Automatically fix linting issues
}

## pre commit hook - Configure Husky 

--> npx husky install

--> npx husky add .husky/pre-commit "npx lint-staged"

--> ensure staged files are only linted
"lint-staged": {
  "*.{js,jsx,ts,tsx}": [
    "eslint --fix", // Fix linting issues
    "prettier --write" // Optional: Format code with Prettier
  ]
}

## --> pre push hook

npx husky add .husky/pre-push "npm run lint && npm run build"



## Update .eslintrc.json
Add Prettier to your ESLint configuration:

{
  "extends": [
    "next",
    "next/core-web-vitals",
    "eslint:recommended",
    "plugin:react/recommended",
    "plugin:import/recommended",
    "plugin:prettier/recommended" // Add Prettier
  ],
  "plugins": ["react", "import", "prettier"],
  "rules": {
    "prettier/prettier": "error", // Enforce Prettier rules
    "react/react-in-jsx-scope": "off"
  }
}
## Update lint-staged Configuration

"lint-staged": {
  "*.{js,jsx,ts,tsx}": [
    "eslint --fix",
    "prettier --write"
  ]
}

## Final package
{
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "eslint . --ext .js,.jsx,.ts,.tsx",
    "lint:fix": "eslint . --ext .js,.jsx,.ts,.tsx --fix"
  },
  "lint-staged": {
    "*.{js,jsx,ts,tsx}": [
      "eslint --fix",
      "prettier --write"
    ]
  },
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged",
      "pre-push": "npm run lint && npm run build"
    }
  }
}
