# 📧 Gmail SMTP Setup Guide - MACET Seminar Hall Booking

## 🎯 Quick Start with Gmail SMTP (FREE Solution)

This guide will help you set up Gmail SMTP for your MACET Seminar Hall booking app in under 15 minutes - completely FREE!

---

## ✅ Why Gmail SMTP for Universities?

### **Perfect for Educational Institutions**

| Benefit                  | Description                                |
| ------------------------ | ------------------------------------------ |
| 🆓 **Completely FREE**   | No monthly costs vs $240/year for SendGrid |
| 📧 **2000 emails/day**   | More than enough for seminar hall bookings |
| 🏫 **University Domain** | Excellent deliverability with @macet.edu   |
| ⚡ **Quick Setup**       | 15 minutes vs hours for other services     |
| 🔒 **Google Security**   | Enterprise-grade security and reliability  |
| 🎨 **Custom Templates**  | Full control over email design             |

---

## 🚀 Step-by-Step Setup

### Step 1: Prepare Gmail Account

1. **Use Institutional Email**: `admin@macet.edu` or `bookings@macet.edu`
2. **Enable 2-Factor Authentication**:
   - Go to [Google Account Security](https://myaccount.google.com/security)
   - Click "2-Step Verification" → "Get Started"
   - Follow the setup process

### Step 2: Generate App Password

1. **Go to App Passwords**:

   - Visit [Google App Passwords](https://myaccount.google.com/apppasswords)
   - You may need to sign in again

2. **Create New App Password**:

   - Select app: "Mail"
   - Select device: "Other (custom name)"
   - Enter: "MACET Booking App"
   - Click "Generate"

3. **Copy the Password**: You'll get a 16-character password like: `abcd efgh ijkl mnop`

### Step 3: Configure Environment Variables

Create or update your `.env.local` file:

```bash
# Supabase Configuration
EXPO_PUBLIC_SUPABASE_URL=your_supabase_url
EXPO_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key

# Gmail SMTP Configuration
GMAIL_USER=admin@macet.edu
GMAIL_APP_PASSWORD=abcd efgh ijkl mnop
GMAIL_FROM_NAME=Maulana Azad College Of Engineering & Technology
GMAIL_REPLY_TO=admin@macet.edu
```

### Step 4: Install Dependencies

```bash
npm install nodemailer @types/nodemailer
```

### Step 5: Create Gmail Service

Create `services/gmailService.ts`:

```typescript
import nodemailer from "nodemailer";

// Create Gmail transporter
const gmailTransporter = nodemailer.createTransporter({
	service: "gmail",
	auth: {
		user: process.env.GMAIL_USER,
		pass: process.env.GMAIL_APP_PASSWORD,
	},
});

// Email configuration
export const EMAIL_CONFIG = {
	from: `${process.env.GMAIL_FROM_NAME} <${process.env.GMAIL_USER}>`,
	replyTo: process.env.GMAIL_REPLY_TO || process.env.GMAIL_USER,
};

// Send booking confirmation email
export const sendBookingConfirmation = async (bookingData: {
	to: string;
	facultyName: string;
	hallName: string;
	date: string;
	time: string;
	purpose: string;
}) => {
	const mailOptions = {
		from: EMAIL_CONFIG.from,
		to: bookingData.to,
		subject: `✅ Booking Confirmed - ${bookingData.hallName} | Maulana Azad College Of Engineering & Technology`,
		html: `
      <div style="font-family: Arial, sans-serif; max-width: 600px; margin: 0 auto;">
        <div style="background: linear-gradient(135deg, #1e40af 0%, #3b82f6 100%); color: white; padding: 30px; text-align: center;">
          <h1>🏛️ Maulana Azad College Of Engineering & Technology</h1>
          <h2>Seminar Hall Booking Confirmed</h2>
        </div>
        
        <div style="padding: 30px;">
          <h3>Dear ${bookingData.facultyName},</h3>
          
          <div style="background: #10b981; color: white; padding: 10px 20px; border-radius: 25px; display: inline-block; margin: 20px 0;">
            ✅ Booking Confirmed
          </div>
          
          <p>Your seminar hall booking has been successfully confirmed!</p>
          
          <div style="background: #f8fafc; border: 1px solid #e5e7eb; border-radius: 12px; padding: 25px; margin: 20px 0;">
            <h4>📋 Booking Details</h4>
            <p><strong>📍 Hall:</strong> ${bookingData.hallName}</p>
            <p><strong>📅 Date:</strong> ${bookingData.date}</p>
            <p><strong>⏰ Time:</strong> ${bookingData.time}</p>
            <p><strong>🎯 Purpose:</strong> ${bookingData.purpose}</p>
          </div>
          
          <div style="background: #fef3c7; border-left: 4px solid #f59e0b; padding: 20px; margin: 20px 0;">
            <h4>⚠️ Important Guidelines</h4>
            <ul>
              <li>Please arrive 10 minutes before your scheduled time</li>
              <li>Ensure all attendees follow university guidelines</li>
              <li>Contact admin for any changes: ${EMAIL_CONFIG.replyTo}</li>
            </ul>
          </div>
          
          <p>If you have any questions, please contact us at <a href="mailto:${EMAIL_CONFIG.replyTo}">${EMAIL_CONFIG.replyTo}</a></p>
        </div>
        
        <div style="background: #f9fafb; padding: 25px; text-align: center; color: #6b7280;">
          <p>© 2025 Maulana Azad College Of Engineering & Technology. All rights reserved.</p>
        </div>
      </div>
    `,
		replyTo: EMAIL_CONFIG.replyTo,
	};

	try {
		const info = await gmailTransporter.sendMail(mailOptions);
		console.log("Email sent successfully:", info.messageId);
		return { success: true, messageId: info.messageId };
	} catch (error) {
		console.error("Email sending failed:", error);
		return { success: false, error: error.message };
	}
};

// Test the connection
export const testEmailConnection = async () => {
	try {
		await gmailTransporter.verify();
		console.log("✅ Gmail SMTP connection successful!");
		return true;
	} catch (error) {
		console.error("❌ Gmail SMTP connection failed:", error);
		return false;
	}
};
```

### Step 6: Test Your Setup

Create a test file `testEmail.js`:

```javascript
require("dotenv").config();
const {
	sendBookingConfirmation,
	testEmailConnection,
} = require("./services/gmailService");

async function testSetup() {
	// Test connection
	const connectionTest = await testEmailConnection();

	if (connectionTest) {
		// Test sending email
		const result = await sendBookingConfirmation({
			to: "your-test-email@gmail.com",
			facultyName: "Dr. Test Faculty",
			hallName: "Conference Hall A",
			date: "January 15, 2025",
			time: "10:00 AM - 12:00 PM",
			purpose: "Faculty Meeting",
		});

		console.log("Test result:", result);
	}
}

testSetup();
```

Run the test:

```bash
node testEmail.js
```

---

## 🔧 React Native Integration

### Hook for Email Notifications

```typescript
// hooks/useEmailNotifications.ts
import { useMutation } from "@tanstack/react-query";
import { sendBookingConfirmation } from "../services/gmailService";

export const useEmailNotifications = () => {
	const sendConfirmation = useMutation({
		mutationFn: async (bookingData: {
			to: string;
			facultyName: string;
			hallName: string;
			date: string;
			time: string;
			purpose: string;
		}) => {
			return await sendBookingConfirmation(bookingData);
		},
	});

	return { sendConfirmation };
};
```

### Usage in Components

```typescript
// components/BookingButton.tsx
import React from "react";
import { TouchableOpacity, Text, Alert } from "react-native";
import { useEmailNotifications } from "../hooks/useEmailNotifications";

export const BookingButton = ({ booking, faculty, hall }) => {
	const { sendConfirmation } = useEmailNotifications();

	const handleConfirmBooking = async () => {
		try {
			const result = await sendConfirmation.mutateAsync({
				to: faculty.email,
				facultyName: faculty.name,
				hallName: hall.name,
				date: formatDate(booking.date),
				time: `${booking.startTime} - ${booking.endTime}`,
				purpose: booking.purpose,
			});

			if (result.success) {
				Alert.alert("Success!", "Booking confirmed and email sent!");
			}
		} catch (error) {
			Alert.alert("Error", "Failed to send confirmation email");
		}
	};

	return (
		<TouchableOpacity
			onPress={handleConfirmBooking}
			style={{ backgroundColor: "#1E40AF", padding: 15, borderRadius: 8 }}
		>
			<Text style={{ color: "white", textAlign: "center", fontWeight: "bold" }}>
				Confirm & Send Email
			</Text>
		</TouchableOpacity>
	);
};
```

---

## 📊 Monitoring & Analytics

### Simple Email Logging

```typescript
// Add to your gmail service
const logEmail = async (emailData: {
	recipient: string;
	subject: string;
	status: "sent" | "failed";
	messageId?: string;
	error?: string;
}) => {
	// Log to Supabase
	await supabase.from("email_logs").insert({
		recipient_email: emailData.recipient,
		subject: emailData.subject,
		status: emailData.status,
		message_id: emailData.messageId,
		error_message: emailData.error,
		sent_at: new Date().toISOString(),
	});
};
```

### Email Analytics Query

```sql
-- Get email statistics
SELECT
  status,
  COUNT(*) as count,
  DATE(sent_at) as date
FROM email_logs
WHERE sent_at >= NOW() - INTERVAL '30 days'
GROUP BY status, DATE(sent_at)
ORDER BY date DESC;
```

---

## ✅ Verification Checklist

Before going live, verify:

- [ ] Gmail 2FA is enabled
- [ ] App password is generated and stored securely
- [ ] Environment variables are set correctly
- [ ] Test email sends successfully
- [ ] Email appears in recipient's inbox (not spam)
- [ ] Email template looks good on mobile
- [ ] Error handling works properly
- [ ] Email logging is functioning

---

## 🚨 Troubleshooting

### Common Issues & Solutions

| Problem                  | Solution                                          |
| ------------------------ | ------------------------------------------------- |
| "Invalid login" error    | Ensure 2FA is enabled and app password is correct |
| Emails go to spam        | Use your institutional domain (@macet.edu)        |
| Connection timeout       | Check firewall settings, try different network    |
| "Less secure apps" error | Use app password instead of regular password      |
| Daily limit exceeded     | Gmail allows 2000 emails/day - monitor usage      |

### Support Contacts

- **Gmail Issues**: [Google Support](https://support.google.com/mail)
- **Technical Issues**: Contact your IT department
- **App Development**: Check logs and error messages

---

## 💡 Pro Tips

1. **Use Institutional Email**: @macet.edu domain has better deliverability
2. **Monitor Daily Limits**: Gmail allows 2000 emails/day
3. **Template Testing**: Test emails on different devices/clients
4. **Backup Plan**: Have SendGrid as backup if needed
5. **Logging**: Always log email attempts for debugging
6. **Security**: Never commit credentials to code repository

---

**🎉 Congratulations! You now have a completely FREE, professional email system for your seminar hall booking app!**

_Total setup time: ~15 minutes_  
_Monthly cost: $0_  
_Daily email limit: 2000 (more than enough!)_
