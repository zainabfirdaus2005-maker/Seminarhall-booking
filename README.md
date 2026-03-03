# 🏛️ Maulana Azad College Of Engineering & Technology - Seminar Hall Booking App

A modern React Native Expo application designed specifically for Maulana Azad College Of Engineering & Technology to eliminate seminar hall booking conflicts and streamline the reservation process for faculty members.

## 🎯 Project Overview

**Problem**: Faculty members currently book seminar halls via WhatsApp groups, leading to double bookings and scheduling conflicts.

**Solution**: A real-time booking system with conflict prevention, automated email notifications, and streamlined hall management.

## ✨ Key Features

- 🔐 **Role-Based Authentication** - Super Admin, Admin, and Faculty access levels
- 🏢 **Real-Time Hall Availability** - Live conflict detection and prevention
- 📅 **Smart Booking System** - One-time and recurring bookings with equipment selection
- � **Email Notifications** - Automated confirmations via Gmail SMTP (FREE)
- 📱 **Push Notifications** - Real-time alerts through Expo notifications
- 📊 **Admin Dashboard** - Hall management and booking analytics
- 🆓 **Free Booking System** - No payment processing (college use)
- 🎨 **Modern UI/UX** - Clean, intuitive interface optimized for faculty use

## 🛠️ Tech Stack

### **Frontend (Mobile App)**

- **React Native** - Cross-platform mobile framework
- **Expo** - Development platform with OTA updates
- **TypeScript** - Type-safe development
- **Modern StyleSheet** - Custom styling with gradients and animations
- **React Navigation** - Navigation library
- **Zustand** - Lightweight state management
- **TanStack Query** - Server state management
- **React Hook Form** - Form handling with validation
- **React Native Reanimated** - Smooth animations
- **Expo Linear Gradient** - Beautiful UI gradients

### **Backend & Services**

- **Supabase** - PostgreSQL database with real-time subscriptions
- **Supabase Auth** - Authentication with Row Level Security
- **Supabase Edge Functions** - Serverless functions
- **Gmail SMTP** - Email notifications (FREE solution)
- **Expo Notifications** - Push notifications

### **UI/UX Libraries**

- **Expo Vector Icons** - Comprehensive icon library
- **React Native Paper** - Material Design components
- **React Native Calendars** - Calendar integration
- **React Native Gesture Handler** - Touch interactions

## Getting Started

### Prerequisites

- Node.js (v16 or later)
- npm or yarn
- Expo CLI
- iOS Simulator (for iOS development)
- Android Studio & Android Emulator (for Android development)

### Installation

1. Clone the repository:

   ```bash
   git clone <repository-url>
   cd Seminarhall-booking-app
   ```

2. Install dependencies:

   ```bash
   npm install
   ```

3. Start the development server:
   ```bash
   npm start
   ```

### Running the App

- **Web**: Press `w` in the terminal or run `npm run web`
- **iOS**: Press `i` in the terminal or run `npm run ios` (requires macOS)
- **Android**: Press `a` in the terminal or run `npm run android`

## Project Structure

```
src/
├── components/          # Reusable UI components
├── navigation/          # Navigation configuration
│   └── AppNavigator.tsx # Main navigation setup
├── screens/            # App screens
│   ├── HomeScreen.tsx
│   ├── LoginScreen.tsx
│   ├── HallListScreen.tsx
│   ├── BookingScreen.tsx
│   └── ProfileScreen.tsx
├── services/           # API calls and business logic
├── types/             # TypeScript type definitions
│   └── index.ts
└── utils/             # Utility functions
```

## Available Scripts

- `npm start` - Start the Expo development server
- `npm run android` - Run on Android device/emulator
- `npm run ios` - Run on iOS simulator (macOS only)
- `npm run web` - Run in web browser
- `npm run lint` - Run ESLint
- `npm run type-check` - Run TypeScript type checking

## Development Guidelines

### Code Style

- Use TypeScript for all new files
- Follow React Native best practices
- Use functional components with hooks
- Implement proper error handling
- Use meaningful variable and function names

### State Management

- Use React hooks for local state
- Consider Context API for global state
- Implement proper data caching strategies

### UI/UX Guidelines

- Follow Material Design principles
- Ensure accessibility compliance
- Use consistent color scheme and typography
- Implement responsive layouts

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

For support and questions, please contact the development team or create an issue in the repository.
