# hot-to-go
Boilerplate Vue 3 + Docker + PostgreSQL with TDD
my-vue3-app/
├── public/                  # Static files (e.g., index.html, favicon.ico)
│   ├── index.html           # Main HTML file
│   └── favicon.ico          # Favicon
├── src/                     # Application source code
│   ├── assets/              # Static assets (e.g., images, fonts)
│   │   └── logo.png         # Example image
│   ├── components/          # Reusable Vue components
│   │   ├── Header.vue       # Example component
│   │   └── Footer.vue       # Example component
│   ├── views/               # Page-level components (routes)
│   │   ├── HomeView.vue     # Example view
│   │   └── AboutView.vue    # Example view
│   ├── router/              # Vue Router configuration
│   │   └── index.js         # Router setup
│   ├── store/               # Vuex store (state management)
│   │   └── index.js         # Vuex store setup
│   ├── services/            # API services or utilities
│   │   └── api.js           # Example API service
│   ├── styles/              # Global styles (e.g., SCSS, CSS)
│   │   └── global.scss      # Example global styles
│   ├── App.vue              # Root Vue component
│   └── main.js              # Entry point for the application
├── tests/                   # Test files
│   ├── unit/                # Unit tests
│   │   └── example.spec.js  # Example unit test
│   └── e2e/                 # End-to-end tests
│       └── example.spec.js  # Example e2e test
├── .env                     # Environment variables
├── .env.development         # Development environment variables
├── .env.production          # Production environment variables
├── .eslintrc.js             # ESLint configuration
├── .prettierrc              # Prettier configuration
├── babel.config.js          # Babel configuration
├── package.json             # Project dependencies and scripts
├── package-lock.json        # Lock file for dependencies
├── README.md                # Project documentation
└── vue.config.js            # Vue CLI configuration (if using Vue CLI)
