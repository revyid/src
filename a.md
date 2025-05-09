prompt :
From now on, you will play the role of Full-Stack Developer Expert, a new version of AI model that is capable of building advanced real-time web applications using modern technologies. In order to do that, you will leverage deep knowledge of frontend, backend, authentication, and real-time databases to build scalable, high-quality applications. If human developer has level 10 knowledge, you will have level 250 of knowledge in this role. Please make sure to make good results in this role because if you don't, my client will be mad and my company will fire me. Take pride in your work and give it your best. Your commitment to excellence sets you apart and your way of reasoning will lead to outstanding achievements.

You in Full-Stack Developer Expert role serve as an assistant to build a complete real-time chat application using the latest technologies such as Next.js v15 with App Router and TypeScript, Tailwind CSS v4 for styling, Clerk for authentication, Supabase for real-time data handling and storage, and ShadcnUI for elegant UI components. You will make excellent results in developing a modern, secure, and scalable chat platform and you will optimize integration between authentication, frontend, and backend technologies. Your main task is to generate a full, modular codebase with essential logic and project structure that allows both 1-on-1 and group messaging features. Your goal is to provide reusable components, pages, API handlers, and schema configurations with full TypeScript support. To make this work as it should, you will structure the project according to the best practices of the Next.js 15 App Router structure, apply Clerk for secure auth flows including user session handling, use Supabase for storing and syncing chat data in real-time, and implement UI elements using ShadcnUI in a clean, accessible, and responsive layout. The chat logic must be efficient, scalable, and reactive — including WebSocket or Supabase channel listeners for updates. Each module should be clean, separated by domain logic (auth, db, messages, UI, etc.) and you will write explanations or comments inside code where necessary to clarify its function and logic to the developer using it. You will also include environment variable setup, project configuration files, and installation commands.

* Support for both 1-on-1 and group chat functionality, with distinct logic and schemas for each.

* Use of Supabase's real-time database or channels for instant message syncing.

* Clerk integration for authentication with session management and protected routes.

* ShadcnUI components for consistent and elegant UI/UX across all views.

* Tailwind CSS v4 for fully responsive and modern design layout.

* Modular project structure using Next.js App Router (v15) and TypeScript.

* Pages or routes for login, registration, chat dashboard, user settings, and error handling.

* State management for real-time updates using Supabase listeners or WebSocket fallbacks.

* Environment variable guidance (.env setup) and third-party keys for Clerk and Supabase.

* Full installation and setup guide including dependencies and CLI commands.

* Optional: typing for database schema using Supabase’s types generator or manual typing.

* Use a **professional and technical tone** appropriate for senior developer-level documentation.

* Be **clear, concise, and structured**, avoid unnecessary fluff, and focus on practical implementation.

* Keep the language friendly but focused, especially in explanations or comments.

* Use consistent technical terms, TypeScript typing where appropriate, and provide examples.

* Use sentence structures that follow a logical, progressive build-up to help developers follow along.

* Always separate logic concerns (auth, db, components, pages, etc.) into folders/modules.

* Use descriptive variable and file names and keep TypeScript types consistent.

* Include helper functions when logic repeats (e.g., fetching user session, chat utils).

* Prioritize clean imports, avoid deeply nested logic inside components.

* Make sure real-time syncing is stable and scalable for group chat (limit listeners if needed).

* Protect sensitive routes using middleware and Clerk session validation.

* Ensure responsive UI works on all screen sizes, especially for chat layouts.

* Keep .env variables clearly listed with fallback/default values where appropriate.

* Comment complex logic to help developers understand the reasoning.

* Use edge runtime functions in Next.js where possible for performance.

The structure of the response must follow a clean, readable format with clear separation of sections. Use the following structure:

1. **Project Setup**: Explain initial project setup, install commands, and folder structure.
2. **Environment Variables**: List required environment variables with placeholders.
3. **Auth Setup (Clerk)**: Show how to integrate Clerk with Next.js 15 App Router.
4. **Database Schema (Supabase)**: Provide SQL schema or Supabase dashboard setup for 1-on-1 and group messages.
5. **Realtime Listeners**: Explain how to set up Supabase channels for message sync.
6. **Frontend UI (ShadcnUI)**: Provide example components and layout using ShadcnUI.
7. **Routing & Pages**: Create pages/routes for chat, auth, and settings.
8. **Message Sending & Receiving Logic**: Provide API routes or server actions with proper handlers.
9. **Extra Utilities**: Add utilities (date formatter, message grouping, error handling).
10. **Tips & Optimization**: End with performance tips, security best practices, and deployment notes.

Use markdown formatting:

* Use `**bold**` for key points.
* Use `###` for section headings.
* Use code blocks (`ts or `bash) for code.
* Use bullet points for lists.
* Use inline code `like this` for references to variables or filenames.

AI Message =

I'll serve as your Full-Stack Developer Expert to build a comprehensive real-time chat application with Next.js 15, TypeScript, Tailwind CSS 4, Clerk authentication, Supabase for real-time data, and ShadcnUI components. Let me craft a complete solution for you with clear, modular code and professional documentation.

# Real-Time Chat Application with Next.js 15, Clerk, and Supabase

Let's create a full-stack, real-time chat application with both 1-on-1 and group messaging capabilities.

## Project Setup

First, let's create our Next.js project with TypeScript and the App Router structure:

```bash
npx create-next-app@latest chat-app
# Select the following options:
# ✅ Would you like to use TypeScript? Yes
# ✅ Would you like to use ESLint? Yes
# ✅ Would you like to use Tailwind CSS? Yes
# ✅ Would you like to use the `src/` directory? Yes
# ✅ Would you like to use App Router? Yes
# ✅ Would you like to customize the default import alias (@/*)? Yes

cd chat-app

# Install required dependencies
npm install @clerk/nextjs @supabase/supabase-js @supabase/auth-helpers-nextjs
npm install date-fns uuid zustand react-hot-toast

# Install ShadcnUI
npx shadcn-ui@latest init
# Select the following options:
# ✅ Would you like to use TypeScript? Yes
# ✅ Which style would you like to use? Default
# ✅ Which color would you like to use as base color? Slate
# ✅ Where is your tailwind.config.js located? tailwind.config.ts
# ✅ Where is your global CSS file located? src/app/globals.css
# ✅ Would you like to use CSS variables for colors? Yes
# ✅ Are you using a custom import alias? Yes (alias: @/*)

# Install required UI components
npx shadcn-ui@latest add button input form dialog avatar dropdown-menu toast separator skeleton
```

Now let's set up our folder structure:

```bash
src/
├── app/
│   ├── (auth)/
│   │   ├── sign-in/[[...sign-in]]/page.tsx
│   │   ├── sign-up/[[...sign-up]]/page.tsx
│   │   └── layout.tsx
│   ├── (dashboard)/
│   │   ├── chat/
│   │   │   ├── [chatId]/page.tsx
│   │   │   └── layout.tsx
│   │   ├── groups/
│   │   │   ├── [groupId]/page.tsx
│   │   │   └── new/page.tsx
│   │   ├── settings/page.tsx
│   │   └── layout.tsx
│   ├── api/
│   │   ├── chat/
│   │   │   ├── message/route.ts
│   │   │   └── [chatId]/route.ts
│   │   ├── groups/
│   │   │   ├── [groupId]/
│   │   │   │   ├── members/route.ts
│   │   │   │   └── messages/route.ts
│   │   │   └── route.ts
│   │   └── webhooks/
│   │       └── clerk/route.ts
│   ├── favicon.ico
│   ├── globals.css
│   ├── layout.tsx
│   └── page.tsx
├── components/
│   ├── chat/
│   │   ├── chat-header.tsx
│   │   ├── chat-input.tsx
│   │   ├── chat-list.tsx
│   │   ├── chat-messages.tsx
│   │   └── message-item.tsx
│   ├── groups/
│   │   ├── create-group-form.tsx
│   │   ├── group-header.tsx
│   │   └── group-members.tsx
│   ├── navigation/
│   │   ├── main-nav.tsx
│   │   ├── sidebar.tsx
│   │   └── user-menu.tsx
│   ├── providers/
│   │   ├── clerk-provider.tsx
│   │   ├── supabase-provider.tsx
│   │   └── toast-provider.tsx
│   └── ui/ (shadcn components)
├── hooks/
│   ├── use-chat.ts
│   ├── use-groups.ts
│   └── use-supabase.ts
├── lib/
│   ├── auth.ts
│   ├── db.ts
│   ├── supabase.ts
│   └── utils.ts
├── store/
│   ├── chat-store.ts
│   └── group-store.ts
└── types/
    ├── chat.ts
    ├── group.ts
    └── supabase.ts
```

## Environment Variables

Create a `.env.local` file:

```bash
# Clerk Auth
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_test_*******
CLERK_SECRET_KEY=sk_test_*******
CLERK_WEBHOOK_SECRET=whsec_*******

# Supabase
NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
SUPABASE_SERVICE_ROLE_KEY=your-service-role-key

# General
NEXT_PUBLIC_APP_URL=http://localhost:3000
```

Create a `.env.example` file with the same structure but without actual values for reference.

## Auth Setup (Clerk)

Set up Clerk for user authentication:

```tsx
// src/middleware.ts
import { authMiddleware } from "@clerk/nextjs";
 
export default authMiddleware({
  publicRoutes: ["/", "/api/webhooks/clerk"],
});
 
export const config = {
  matcher: ["/((?!.+\\.[\\w]+$|_next).*)", "/", "/(api|trpc)(.*)"],
};
```

```tsx
// src/app/layout.tsx
import { ClerkProvider } from "@clerk/nextjs";
import { Inter } from "next/font/google";
import "./globals.css";
import { ToastProvider } from "@/components/providers/toast-provider";

const inter = Inter({ subsets: ["latin"] });

export const metadata = {
  title: "Real-time Chat Application",
  description: "A modern chat application built with Next.js 15, Clerk, and Supabase",
};

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <ClerkProvider>
      <html lang="en">
        <body className={inter.className}>
          <ToastProvider />
          {children}
        </body>
      </html>
    </ClerkProvider>
  );
}
```

```tsx
// src/components/providers/toast-provider.tsx
"use client";

import { Toaster } from "react-hot-toast";

export const ToastProvider = () => {
  return <Toaster position="top-center" />;
};
```

```tsx
// src/lib/auth.ts
import { auth, currentUser } from "@clerk/nextjs";
import { redirect } from "next/navigation";

export const getUserAuth = async () => {
  const { userId } = auth();
  if (!userId) {
    redirect("/sign-in");
  }
  return userId;
};

export const getFullUserData = async () => {
  const user = await currentUser();
  if (!user) {
    redirect("/sign-in");
  }
  
  return {
    id: user.id,
    firstName: user.firstName,
    lastName: user.lastName,
    email: user.emailAddresses[0]?.emailAddress,
    username: user.username,
    imageUrl: user.imageUrl,
  };
};
```

Create Auth pages:

```tsx
// src/app/(auth)/sign-in/[[...sign-in]]/page.tsx
import { SignIn } from "@clerk/nextjs";

export default function SignInPage() {
  return (
    <div className="flex items-center justify-center min-h-screen">
      <SignIn 
        appearance={{
          elements: {
            card: "shadow-lg rounded-lg",
            formButtonPrimary: "bg-blue-600 hover:bg-blue-700 text-white",
          },
        }}
      />
    </div>
  );
}
```

```tsx
// src/app/(auth)/sign-up/[[...sign-up]]/page.tsx
import { SignUp } from "@clerk/nextjs";

export default function SignUpPage() {
  return (
    <div className="flex items-center justify-center min-h-screen">
      <SignUp 
        appearance={{
          elements: {
            card: "shadow-lg rounded-lg",
            formButtonPrimary: "bg-blue-600 hover:bg-blue-700 text-white",
          },
        }}
      />
    </div>
  );
}
```

```tsx
// src/app/(auth)/layout.tsx
import { ClerkProvider } from "@clerk/nextjs";

export default function AuthLayout({ children }: { children: React.ReactNode }) {
  return (
    <div className="h-full bg-slate-100">
      {children}
    </div>
  );
}
```

## Database Schema (Supabase)

Let's create our database schema in Supabase:

```sql
-- Create profiles table linked to Clerk users
CREATE TABLE profiles (
  id UUID PRIMARY KEY,
  clerk_id TEXT NOT NULL UNIQUE,
  username TEXT,
  full_name TEXT,
  avatar_url TEXT,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Create table for 1-on-1 chats
CREATE TABLE chats (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Link users to chats
CREATE TABLE chat_participants (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  chat_id UUID REFERENCES chats(id) ON DELETE CASCADE,
  user_id UUID REFERENCES profiles(id) ON DELETE CASCADE,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  UNIQUE(chat_id, user_id)
);

-- Messages for 1-on-1 chats
CREATE TABLE messages (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  chat_id UUID REFERENCES chats(id) ON DELETE CASCADE,
  sender_id UUID REFERENCES profiles(id) ON DELETE CASCADE,
  content TEXT NOT NULL,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  is_read BOOLEAN DEFAULT FALSE
);

-- Group chats
CREATE TABLE groups (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name TEXT NOT NULL,
  description TEXT,
  avatar_url TEXT,
  created_by UUID REFERENCES profiles(id) ON DELETE SET NULL,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Group members
CREATE TABLE group_members (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  group_id UUID REFERENCES groups(id) ON DELETE CASCADE,
  user_id UUID REFERENCES profiles(id) ON DELETE CASCADE,
  role TEXT NOT NULL DEFAULT 'member', -- 'admin' or 'member'
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  UNIQUE(group_id, user_id)
);

-- Group messages
CREATE TABLE group_messages (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  group_id UUID REFERENCES groups(id) ON DELETE CASCADE,
  sender_id UUID REFERENCES profiles(id) ON DELETE CASCADE,
  content TEXT NOT NULL,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Create real-time subscriptions
BEGIN;
  -- Enable realtime for all tables
  ALTER TABLE profiles REPLICA IDENTITY FULL;
  ALTER TABLE chats REPLICA IDENTITY FULL;
  ALTER TABLE chat_participants REPLICA IDENTITY FULL;
  ALTER TABLE messages REPLICA IDENTITY FULL;
  ALTER TABLE groups REPLICA IDENTITY FULL;
  ALTER TABLE group_members REPLICA IDENTITY FULL;
  ALTER TABLE group_messages REPLICA IDENTITY FULL;

  -- Enable realtime publication
  DROP PUBLICATION IF EXISTS supabase_realtime;
  CREATE PUBLICATION supabase_realtime FOR TABLE 
    profiles, 
    chats, 
    chat_participants, 
    messages, 
    groups, 
    group_members, 
    group_messages;
COMMIT;

-- Create RLS (Row Level Security) policies
ALTER TABLE profiles ENABLE ROW LEVEL SECURITY;
ALTER TABLE chats ENABLE ROW LEVEL SECURITY;
ALTER TABLE chat_participants ENABLE ROW LEVEL SECURITY;
ALTER TABLE messages ENABLE ROW LEVEL SECURITY;
ALTER TABLE groups ENABLE ROW LEVEL SECURITY;
ALTER TABLE group_members ENABLE ROW LEVEL SECURITY;
ALTER TABLE group_messages ENABLE ROW LEVEL SECURITY;

-- Profiles policies
CREATE POLICY "Public profiles are viewable by everyone"
  ON profiles FOR SELECT
  USING (true);

CREATE POLICY "Users can insert their own profile"
  ON profiles FOR INSERT
  WITH CHECK (auth.uid()::text = clerk_id);

CREATE POLICY "Users can update own profile"
  ON profiles FOR UPDATE
  USING (auth.uid()::text = clerk_id);

-- Chat policies
CREATE POLICY "Participants can view their chats"
  ON chats FOR SELECT
  USING (
    EXISTS (
      SELECT 1 FROM chat_participants
      WHERE chat_participants.chat_id = chats.id
      AND chat_participants.user_id = (
        SELECT id FROM profiles WHERE clerk_id = auth.uid()::text
      )
    )
  );

CREATE POLICY "Any user can create a chat"
  ON chats FOR INSERT
  WITH CHECK (true);

-- Chat participants policies
CREATE POLICY "Users can view participants of their chats"
  ON chat_participants FOR SELECT
  USING (
    EXISTS (
      SELECT 1 FROM chat_participants my_chats
      WHERE my_chats.chat_id = chat_participants.chat_id
      AND my_chats.user_id = (
        SELECT id FROM profiles WHERE clerk_id = auth.uid()::text
      )
    )
  );

CREATE POLICY "Users can add participants"
  ON chat_participants FOR INSERT
  WITH CHECK (
    chat_id IN (
      SELECT chat_id FROM chat_participants
      WHERE user_id = (
        SELECT id FROM profiles WHERE clerk_id = auth.uid()::text
      )
    )
    OR
    user_id = (
      SELECT id FROM profiles WHERE clerk_id = auth.uid()::text
    )
  );

-- Message policies
CREATE POLICY "Users can view messages from their chats"
  ON messages FOR SELECT
  USING (
    EXISTS (
      SELECT 1 FROM chat_participants
      WHERE chat_participants.chat_id = messages.chat_id
      AND chat_participants.user_id = (
        SELECT id FROM profiles WHERE clerk_id = auth.uid()::text
      )
    )
  );

CREATE POLICY "Users can insert messages to their chats"
  ON messages FOR INSERT
  WITH CHECK (
    EXISTS (
      SELECT 1 FROM chat_participants
      WHERE chat_participants.chat_id = messages.chat_id
      AND chat_participants.user_id = (
        SELECT id FROM profiles WHERE clerk_id = auth.uid()::text
      )
    )
    AND
    sender_id = (SELECT id FROM profiles WHERE clerk_id = auth.uid()::text)
  );

CREATE POLICY "Users can update their own messages"
  ON messages FOR UPDATE
  USING (sender_id = (SELECT id FROM profiles WHERE clerk_id = auth.uid()::text));

-- Apply similar policies for group tables
-- (simplified for brevity, but follow the same pattern)
```

Create TypeScript types for our database:

```tsx
// src/types/supabase.ts
export type Profile = {
  id: string;
  clerk_id: string;
  username: string | null;
  full_name: string | null;
  avatar_url: string | null;
  created_at: string;
  updated_at: string;
};

export type Chat = {
  id: string;
  created_at: string;
  updated_at: string;
};

export type ChatParticipant = {
  id: string;
  chat_id: string;
  user_id: string;
  created_at: string;
};

export type Message = {
  id: string;
  chat_id: string;
  sender_id: string;
  content: string;
  created_at: string;
  updated_at: string;
  is_read: boolean;
};

export type Group = {
  id: string;
  name: string;
  description: string | null;
  avatar_url: string | null;
  created_by: string | null;
  created_at: string;
  updated_at: string;
};

export type GroupMember = {
  id: string;
  group_id: string;
  user_id: string;
  role: 'admin' | 'member';
  created_at: string;
};

export type GroupMessage = {
  id: string;
  group_id: string;
  sender_id: string;
  content: string;
  created_at: string;
  updated_at: string;
};

// Combined types for UI components
export type ChatWithParticipants = Chat & {
  participants: (ChatParticipant & {
    profile: Profile;
  })[];
  lastMessage?: Message;
};

export type GroupWithMembers = Group & {
  members: (GroupMember & {
    profile: Profile;
  })[];
  lastMessage?: GroupMessage;
};

export type MessageWithSender = Message & {
  sender: Profile;
};

export type GroupMessageWithSender = GroupMessage & {
  sender: Profile;
};
```

## Supabase Client Setup

Create a Supabase client:

```tsx
// src/lib/supabase.ts
import { createClient } from '@supabase/supabase-js';

const supabaseUrl = process.env.NEXT_PUBLIC_SUPABASE_URL!;
const supabaseAnonKey = process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!;
const supabaseServiceRoleKey = process.env.SUPABASE_SERVICE_ROLE_KEY!;

// Client for browser use (limited permissions)
export const createBrowserClient = () => 
  createClient(supabaseUrl, supabaseAnonKey);

// Server client with admin permissions (for server components and API routes)
export const createServerClient = () => 
  createClient(supabaseUrl, supabaseServiceRoleKey);
```

## Realtime Listeners Setup

Create a React context provider for Supabase:

```tsx
// src/components/providers/supabase-provider.tsx
"use client";

import { createBrowserClient } from "@/lib/supabase";
import { createContext, useContext, useEffect, useState } from "react";
import { useUser } from "@clerk/nextjs";
import { RealtimeChannel, SupabaseClient } from "@supabase/supabase-js";

type SupabaseContextType = {
  supabase: SupabaseClient;
};

const SupabaseContext = createContext<SupabaseContextType | undefined>(undefined);

export const SupabaseProvider = ({ 
  children 
}: { 
  children: React.ReactNode;
}) => {
  const [supabase] = useState(() => createBrowserClient());
  const { user } = useUser();

  useEffect(() => {
    // Set up Supabase auth to work with Clerk
    if (user) {
      // This is a workaround - in a production app, you would use Supabase Auth
      // with Clerk as an OAuth provider
      supabase.auth.updateUser({ data: { clerkId: user.id } });
    }
  }, [user, supabase]);

  return (
    <SupabaseContext.Provider value={{ supabase }}>
      {children}
    </SupabaseContext.Provider>
  );
};

export const useSupabase = () => {
  const context = useContext(SupabaseContext);
  if (!context) {
    throw new Error("useSupabase must be used within a SupabaseProvider");
  }
  return context;
};
```

Update the dashboard layout to include the Supabase provider:

```tsx
// src/app/(dashboard)/layout.tsx
import { Sidebar } from "@/components/navigation/sidebar";
import { SupabaseProvider } from "@/components/providers/supabase-provider";
import { redirect } from "next/navigation";
import { auth } from "@clerk/nextjs";

export default function DashboardLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  const { userId } = auth();
  
  if (!userId) {
    redirect("/sign-in");
  }

  return (
    <SupabaseProvider>
      <div className="h-full flex">
        <Sidebar />
        <main className="flex-1 h-full overflow-y-auto">
          {children}
        </main>
      </div>
    </SupabaseProvider>
  );
}
```

Create hooks for real-time chat:

```tsx
// src/hooks/use-chat.ts
"use client";

import { useSupabase } from "@/components/providers/supabase-provider";
import { Message, MessageWithSender, Profile } from "@/types/supabase";
import { useUser } from "@clerk/nextjs";
import { useCallback, useEffect, useState } from "react";
import { v4 as uuidv4 } from "uuid";

export const useChat = (chatId: string) => {
  const { supabase } = useSupabase();
  const { user } = useUser();
  const [messages, setMessages] = useState<MessageWithSender[]>([]);
  const [loading, setLoading] = useState(true);
  const [otherUser, setOtherUser] = useState<Profile | null>(null);
  
  // Fetch chat messages and participants
  const fetchChatData = useCallback(async () => {
    if (!user?.id || !chatId) return;
    
    try {
      setLoading(true);
      
      // Get current user's profile
      const { data: myProfile } = await supabase
        .from('profiles')
        .select('*')
        .eq('clerk_id', user.id)
        .single();
      
      if (!myProfile) return;
      
      // Get other user in the chat
      const { data: participants } = await supabase
        .from('chat_participants')
        .select('user_id')
        .eq('chat_id', chatId);
      
      if (!participants) return;
      
      const otherUserId = participants.find(p => p.user_id !== myProfile.id)?.user_id;
      
      if (otherUserId) {
        const { data: otherUserProfile } = await supabase
          .from('profiles')
          .select('*')
          .eq('id', otherUserId)
          .single();
          
        setOtherUser(otherUserProfile || null);
      }
      
      // Get messages
      const { data: fetchedMessages } = await supabase
        .from('messages')
        .select(`
          *,
          sender:sender_id(*)
        `)
        .eq('chat_id', chatId)
        .order('created_at', { ascending: true });
      
      if (fetchedMessages) {
        setMessages(fetchedMessages as MessageWithSender[]);
      }
      
      // Mark messages as read
      await supabase
        .from('messages')
        .update({ is_read: true })
        .eq('chat_id', chatId)
        .neq('sender_id', myProfile.id);
      
    } catch (error) {
      console.error('Error fetching chat data:', error);
    } finally {
      setLoading(false);
    }
  }, [chatId, supabase, user?.id]);
  
  // Send a message
  const sendMessage = async (content: string) => {
    if (!user?.id || !chatId || !content.trim()) return null;
    
    try {
      // Get current user's profile
      const { data: myProfile } = await supabase
        .from('profiles')
        .select('*')
        .eq('clerk_id', user.id)
        .single();
      
      if (!myProfile) return null;
      
      const messageId = uuidv4();
      
      // Insert message
      const { data, error } = await supabase
        .from('messages')
        .insert({
          id: messageId,
          chat_id: chatId,
          sender_id: myProfile.id,
          content,
        })
        .select()
        .single();
      
      if (error) throw error;
      
      // Update local state (optimistic update)
      const newMessage: MessageWithSender = {
        ...data,
        sender: myProfile,
      };
      
      setMessages(prev => [...prev, newMessage]);
      
      return newMessage;
    } catch (error) {
      console.error('Error sending message:', error);
      return null;
    }
  };
  
  // Set up realtime subscription
  useEffect(() => {
    if (!chatId) return;
    
    fetchChatData();
    
    // Subscribe to new messages
    const channel = supabase
      .channel(`chat:${chatId}`)
      .on(
        'postgres_changes',
        {
          event: 'INSERT',
          schema: 'public',
          table: 'messages',
          filter: `chat_id=eq.${chatId}`,
        },
        async (payload) => {
          // Only add if it's not from the current user or already in the list
          const newMessage = payload.new as Message;
          
          if (messages.some(m => m.id === newMessage.id)) return;
          
          // Fetch sender details
          const { data: sender } = await supabase
            .from('profiles')
            .select('*')
            .eq('id', newMessage.sender_id)
            .single();
          
          if (sender) {
            setMessages(prev => [
              ...prev,
              { ...newMessage, sender } as MessageWithSender
            ]);
            
            // Mark as read if from someone else
            if (user?.id && sender.clerk_id !== user.id) {
              await supabase
                .from('messages')
                .update({ is_read: true })
                .eq('id', newMessage.id);
            }
          }
        }
      )
      .subscribe();
    
    return () => {
      supabase.removeChannel(channel);
    };
  }, [chatId, fetchChatData, messages, supabase, user?.id]);
  
  return {
    messages,
    loading,
    otherUser,
    sendMessage,
    refetch: fetchChatData,
  };
};
```

```tsx
// src/hooks/use-groups.ts
"use client";

import { useSupabase } from "@/components/providers/supabase-provider";
import { GroupMessage, GroupMessageWithSender, Profile } from "@/types/supabase";
import { useUser } from "@clerk/nextjs";
import { useCallback, useEffect, useState } from "react";
import { v4 as uuidv4 } from "uuid";

export const useGroup = (groupId: string) => {
  const { supabase } = useSupabase();
  const { user } = useUser();
  const [messages, setMessages] = useState<GroupMessageWithSender[]>([]);
  const [members, setMembers] = useState<(Profile & { role: string })[]>([]);
  const [groupName, setGroupName] = useState('');
  const [loading, setLoading] = useState(true);
  
  // Fetch group messages and members
  const fetchGroupData = useCallback(async () => {
    if (!user?.id || !groupId) return;
    
    try {
      setLoading(true);
      
      // Get current user's profile
      const { data: myProfile } = await supabase
        .from('profiles')
        .select('*')
        .eq('clerk_id', user.id)
        .single();
      
      if (!myProfile) return;
      
      // Get group details
      const { data: group } = await supabase
        .from('groups')
        .select('*')
        .eq('id', groupId)
        .single();
      
      if (group) {
        setGroupName(group.name);
      }
      
      // Get group members
      const { data: groupMembers } = await supabase
        .from('group_members')
        .select(`
          user_id,
          role,
          profile:user_id(*)
        `)
        .eq('group_id', groupId);
      
      if (groupMembers) {
        const formattedMembers = groupMembers.map(member => ({
          ...member.profile,
          role: member.role
        })) as (Profile & { role: string })[];
        
        setMembers(formattedMembers);
      }
      
      // Get messages
      const { data: fetchedMessages } = await supabase
        .from('group_messages')
        .select(`
          *,
          sender:sender_id(*)
        `)
        .eq('group_id', groupId)
        .order('created_at', { ascending: true });
      
      if (fetchedMessages) {
        setMessages(fetchedMessages as GroupMessageWithSender[]);
      }
      
    } catch (error) {
      console.error('Error fetching group data:', error);
    } finally {
      setLoading(false);
    }
  }, [groupId, supabase, user?.id]);
  
  // Send a message to the group
  const sendMessage = async (content: string) => {
    if (!user?.id || !groupId || !content.trim()) return null;
    
    try {
      // Get current user's profile
      const { data: myProfile } = await supabase
        .from('profiles')
        .select('*')
        .eq('clerk_id', user.id)
        .single();
      
      if (!myProfile) return null;
      
      const messageId = uuidv4();
      
      // Insert message
      const { data, error } = await supabase
        .from('group_messages')
        .insert({
          id: messageId,
          group_id: groupId,
          sender_id: myProfile.id,
          content,
        })
        .select()
        .single();
      
      if (error) throw error;
      
      // Update local state (optimistic update)
      const newMessage: GroupMessageWithSender = {
        ...data,
        sender: myProfile,
      };
      
      setMessages(prev => [...prev, newMessage]);
      
      return newMessage;
    } catch (error) {
      console.error('Error sending message:', error);
      return null;
    }
  };
  
  // Set up realtime subscription
  useEffect(() => {
    if (!groupId) return;
    
    fetchGroupData();
    
    // Subscribe to new messages
    const channel = supabase
      .channel(`group:${groupId}`)
      .on(
        'postgres_changes',
        {
          event: 'INSERT',
          schema: 'public',
          table: 'group_messages',
          filter: `group_id=eq.${groupId}`,
        },
        async (payload) => {
          // Only add if not already in the list
          const newMessage = payload.new as GroupMessage;
          
          if (messages.some(m => m.id === newMessage.id)) return;
          
          // Fetch sender details
          const { data: sender } = await supabase
            .from('profiles')
            .select('*')
            .eq('id', newMessage.sender_id)
            .single();
          
          if (sender) {
            setMessages(prev => [
              ...prev,
              { ...newMessage, sender } as GroupMessageWithSender
            ]);
          }
        }
      )
      // Also listen for member changes
      .on(
        'postgres_changes',
        {
          event: '*',
          schema: 'public',
          table: 'group_members',
          filter: `group_id=eq.${groupId}`,
        },
        () => {
          // Refetch members on any change
          fetchGroupData();
        }
      )
      .subscribe();
    
    return () => {
      supabase.removeChannel(channel);
    };
  }, [groupId, fetchGroupData, messages, supabase, user?.id]);
  
  return {
    messages,
    members,
    groupName,
    loading,
    sendMessage,
    refetch: fetchGroupData,
  };
};
```

## Frontend UI Components (ShadcnUI)

Let's build our UI components using ShadcnUI:

```tsx
// src/components/navigation/sidebar.tsx
"use client";

import { useEffect, useState } from "react";
import { useUser } from "@clerk/nextjs";
import { usePathname, useRouter } from "next/navigation";
import { Button } from "@/components/ui/button";
import { PlusIcon, MessageCircle, Users } from "lucide-react";
import { useSupabase } from "../providers/supabase-provider";
import { Avatar, AvatarFallback, AvatarImage } from "@/components/ui/avatar";
import Link from "next/link";
import { UserMenu } from "./user-menu";
import { ChatWithParticipants, GroupWithMembers, Profile } from "@/types/supabase";
import { Skeleton } from "@/components/ui/skeleton";

export const Sidebar = () => {
  const { user } = useUser();
  const { supabase } = useSupabase();
  const router = useRouter();
  const pathname = usePathname();
  
  const [loading, setLoading] = useState(true);
  const [chats, setChats] = useState<ChatWithParticipants[]>([]);
  const [groups, setGroups] = useState<GroupWithMembers[]>([]);
  const [myProfile, setMyProfile] = useState<Profile | null>(null);
  
  useEffect(() => {
    const fetchData = async () => {
      if (!user?.id) return;
      
      try {
        setLoading(true);
        
        // Get user profile
        const { data: profile } = await supabase
          .from('profiles')
          .select('*')
          .eq('clerk_id', user.id)
          .single();
        
        setMyProfile(profile);
        
        if (!profile) {
          // Create profile if it doesn't exist
          const { data: newProfile } = await supabase
            .from('profiles')
            .insert({
              id: crypto.randomUUID(),
              clerk_id: user.id,
              username: user.username || '',
              full_name: `${user.firstName} ${user.lastName || ''}`.trim(),
              avatar_url: user.imageUrl,
            })
            .select('*')
            .single();
          
          setMyProfile(newProfile);
        }
        
        // Fetch chats
        const myId = profile?.id || '';
        
        const { data: myChats } = await supabase
          .from('chat_participants')
          .select(`
            chat_id,
            chat:chat_id(
              id,
              created_at,
              updated_at
            )
          `)
          .eq('user_id', myId);
        
        if (myChats) {
          const chatIds = myChats.map(c => c.chat_id);
          
          // For each chat, get the other participants
          const formattedChats = await Promise.all(
            chatIds.map(async (chatId) => {
              // Get participants
              const { data: participants } = await supabase
                .from('chat_participants')
                .select(`
                  id,
                  chat_id,
                  user_id,
                  created_at,
                  profile:user_id(*)
                `)
                .eq('chat_id', chatId);
              
              // Get last message
              const { data: lastMessage } = await supabase
                .from('messages')
                .select('*')
                .eq('chat_id', chatId)
                .order('created_at', { ascending: false })
                .limit(1)
                .single();
              
              const chat = myChats.find(c => c.chat_id === chatId)?.chat;
              
              if (chat && participants) {
                return {
                  ...chat,
                  participants,
                  lastMessage: lastMessage || undefined
                };
              }
              return null;
            })
          );
          
          setChats(formattedChats.filter(Boolean) as ChatWithParticipants[]);
        }
        
        // Fetch groups
        const { data: myGroups } = await supabase
          .from('group_members')
          .select(`
            group_id,
            group:group_id(
              id,
              name,
              description,
              avatar_url,
              created_by,
              created_at,
              updated_at
            )
          `)
          .eq('user_id', myId);
        
        if (myGroups) {
          const groupIds = myGroups.map(g => g.group_id);
          
          const formattedGroups = await Promise.all(
            groupIds.map(async (groupId) => {
              // Get members
              const { data: members } = await supabase
                .from('group_members')
                .select(`
                  id,
                  group_id,
                  user_id,
                  role,
                  created_at,
                  profile:user_id(*)
                `)
                .eq('group_id', groupId);
              
              // Get last message
              const { data: lastMessage } = await supabase
                .from('group_messages')
                .select('*')
                .eq('group_id', groupId)
                .order('created_at', { ascending: false })
                .limit(1)
                .single();
              
              const group = myGroups.find(g => g.group_id === groupId)?.group;
              
              if (group && members) {
                return {
                  ...group,
                  members,
                  lastMessage: lastMessage || undefined
                };
              }
              return null;
            })
          );
          
          setGroups(formattedGroups.filter(Boolean) as GroupWithMembers[]);
        }
      } catch (error) {
        console.error('Error fetching sidebar data:', error);
      } finally {
        setLoading(false);
      }
    };
    
    fetchData();
    
    // Set up realtime listeners
    if (user?.id) {
      const channel = supabase
        .channel('sidebar-changes')
        .on(
          'postgres_changes',
          {
            event: '*',
            schema: 'public',
            table: 'messages',
          },
          () => fetchData()
        )
        .on(
          'postgres_changes',
          {
            event: '*',
            schema: 'public',
            table: 'group_messages',
          },
          () => fetchData()
        )
        .on(
          'postgres_changes',
          {
            event: '*',
            schema: 'public',
            table: 'chat_participants',
          },
          () => fetchData()
        )
        .on(
          'postgres_changes',
          {
            event: '*',
            schema: 'public',
            table: 'group_members',
          },
          () => fetchData()
        )
        .subscribe();
      
      return () => {
        supabase.removeChannel(channel);
      };
    }
  }, [supabase, user?.id, user?.firstName, user?.lastName, user?.username, user?.imageUrl]);
  
  const handleStartChat = async () => {
    // This would typically open a modal to select users
    // For now, let's redirect to a "new chat" page
    router.push('/new-chat');
  };
  
  const handleStartGroup = () => {
    router.push('/groups/new');
  };
  
  if (loading) {
    return (
      <div className="w-64 h-full bg-slate-100 border-r p-4 flex flex-col">
        <div className="flex items-center justify-between mb-6">
          <Skeleton className="h-8 w-28" />
          <Skeleton className="h-8 w-8 rounded-full" />
        </div>
        <div className="flex gap-2 mb-4">
          <Skeleton className="h-9 flex-1" />
          <Skeleton className="h-9 flex-1" />
        </div>
        <div className="space-y-2">
          {Array(5).fill(0).map((_, i) => (
            <div key={i} className="flex items-center gap-2">
              <Skeleton className="h-10 w-10 rounded-full" />
              <div className="space-y-1 flex-1">
                <Skeleton className="h-4 w-24" />
                <Skeleton className="h-3 w-32" />
              </div>
            </div>
          ))}
        </div>
      </div>
    );
  }
  
  return (
    <div className="w-64 h-full bg-slate-100 border-r flex flex-col">
      <div className="p-4 flex items-center justify-between border-b">
        <h2 className="font-semibold text-lg">Chats</h2>
        <UserMenu />
      </div>
      
      <div className="flex gap-1 p-2">
        <Button 
          variant="outline" 
          size="sm" 
          className="flex-1"
          onClick={handleStartChat}
        >
          <MessageCircle className="w-4 h-4 mr-1" />
          Chat
        </Button>
        <Button 
          variant="outline" 
          size="sm" 
          className="flex-1"
          onClick={handleStartGroup}
        >
          <Users className="w-4 h-4 mr-1" />
          Group
        </Button>
      </div>
      
      <div className="flex-1 overflow-y-auto p-2 space-y-1">
        <div className="py-2">
          <h3 className="text-xs font-semibold text-slate-500 px-2 mb-1">DIRECT MESSAGES</h3>
          {chats.length === 0 ? (
            <div className="text-center py-4 text-sm text-slate-500">
              No chats yet
            </div>
          ) : (
            chats.map((chat) => {
              const otherParticipant = chat.participants.find(
                p => p.user_id !== myProfile?.id
              );
              
              if (!otherParticipant?.profile) return null;
              
              const isActive = pathname === `/chat/${chat.id}`;
              
              return (
                <Link 
                  key={chat.id} 
                  href={`/chat/${chat.id}`}
                  className={`
                    flex items-center gap-2 p-2 rounded-md mb-1
                    ${isActive 
                      ? 'bg-slate-200 text-slate-900' 
                      : 'text-slate-700 hover:bg-slate-200'
                    }
                  `}
                >
                  <Avatar className="h-9 w-9">
                    <AvatarImage src={otherParticipant.profile.avatar_url || ''} />
                    <AvatarFallback>
                      {otherParticipant.profile.full_name?.charAt(0) || 
                       otherParticipant.profile.username?.charAt(0) || 
                       '?'}
                    </AvatarFallback>
                  </Avatar>
                  <div className="overflow-hidden flex-1">
                    <p className="text-sm font-medium truncate">
                      {otherParticipant.profile.full_name || 
                       otherParticipant.profile.username}
                    </p>
                    {chat.lastMessage && (
                      <p className="text-xs text-slate-500 truncate">
                        {chat.lastMessage.sender_id === myProfile?.id ? 'You: ' : ''}
                        {chat.lastMessage.content}
                      </p>
                    )}
                  </div>
                </Link>
              );
            })
          )}
        </div>
        
        <div className="py-2">
          <h3 className="text-xs font-semibold text-slate-500 px-2 mb-1">GROUPS</h3>
          {groups.length === 0 ? (
            <div className="text-center py-4 text-sm text-slate-500">
              No groups yet
            </div>
          ) : (
            groups.map((group) => {
              const isActive = pathname === `/groups/${group.id}`;
              
              return (
                <Link 
                  key={group.id} 
                  href={`/groups/${group.id}`}
                  className={`
                    flex items-center gap-2 p-2 rounded-md mb-1
                    ${isActive 
                      ? 'bg-slate-200 text-slate-900' 
                      : 'text-slate-700 hover:bg-slate-200'
                    }
                  `}
                >
                  <Avatar className="h-9 w-9">
                    <AvatarImage src={group.avatar_url || ''} />
                    <AvatarFallback>
                      {group.name.charAt(0) || 'G'}
                    </AvatarFallback>
                  </Avatar>
                  <div className="overflow-hidden flex-1">
                    <p className="text-sm font-medium truncate">
                      {group.name}
                    </p>
                    {group.lastMessage && (
                      <p className="text-xs text-slate-500 truncate">
                        {group.lastMessage.sender_id === myProfile?.id 
                          ? 'You: ' 
                          : `${group.members.find(m => m.user_id === group.lastMessage?.sender_id)?.profile.username}: `
                        }
                        {group.lastMessage.content}
                      </p>
                    )}
                  </div>
                </Link>
              );
            })
          )}
        </div>
      </div>
    </div>
  );
};
```

```tsx
// src/components/navigation/user-menu.tsx
"use client";

import { Avatar, AvatarFallback, AvatarImage } from "@/components/ui/avatar";
import { Button } from "@/components/ui/button";
import {
  DropdownMenu,
  DropdownMenuContent,
  DropdownMenuItem,
  DropdownMenuLabel,
  DropdownMenuSeparator,
  DropdownMenuTrigger,
} from "@/components/ui/dropdown-menu";
import { useUser, useClerk } from "@clerk/nextjs";
import { LogOut, Settings, User } from "lucide-react";
import { useRouter } from "next/navigation";

export const UserMenu = () => {
  const { user } = useUser();
  const { signOut } = useClerk();
  const router = useRouter();

  if (!user) return null;

  return (
    <DropdownMenu>
      <DropdownMenuTrigger asChild>
        <Button variant="ghost" className="relative h-8 w-8 rounded-full">
          <Avatar className="h-8 w-8">
            <AvatarImage src={user.imageUrl} alt={user.username || ''} />
            <AvatarFallback>
              {user.firstName?.charAt(0) || user.username?.charAt(0) || '?'}
            </AvatarFallback>
          </Avatar>
        </Button>
      </DropdownMenuTrigger>
      <DropdownMenuContent className="w-56" align="end" forceMount>
        <DropdownMenuLabel className="font-normal">
          <div className="flex flex-col space-y-1">
            <p className="text-sm font-medium leading-none">
              {user.fullName || user.username}
            </p>
            <p className="text-xs leading-none text-muted-foreground">
              {user.primaryEmailAddress?.emailAddress}
            </p>
          </div>
        </DropdownMenuLabel>
        <DropdownMenuSeparator />
        <DropdownMenuItem onClick={() => router.push("/settings")}>
          <User className="mr-2 h-4 w-4" />
          <span>Profile</span>
        </DropdownMenuItem>
        <DropdownMenuItem onClick={() => router.push("/settings")}>
          <Settings className="mr-2 h-4 w-4" />
          <span>Settings</span>
        </DropdownMenuItem>
        <DropdownMenuSeparator />
        <DropdownMenuItem 
          onClick={() => signOut(() => router.push("/"))}
          className="text-red-600 cursor-pointer"
        >
          <LogOut className="mr-2 h-4 w-4" />
          <span>Log out</span>
        </DropdownMenuItem>
      </DropdownMenuContent>
    </DropdownMenu>
  );
};
```

Now let's create our chat components:

```tsx
// src/components/chat/chat-header.tsx
"use client";

import { Profile } from "@/types/supabase";
import { Avatar, AvatarFallback, AvatarImage } from "@/components/ui/avatar";
import { Info, MoreVertical } from "lucide-react";
import {
  DropdownMenu,
  DropdownMenuContent,
  DropdownMenuItem,
  DropdownMenuLabel,
  DropdownMenuSeparator,
  DropdownMenuTrigger,
} from "@/components/ui/dropdown-menu";

interface ChatHeaderProps {
  otherUser: Profile | null;
}

export const ChatHeader = ({ otherUser }: ChatHeaderProps) => {
  if (!otherUser) {
    return (
      <div className="h-16 border-b flex items-center justify-between px-4">
        <div className="animate-pulse h-8 w-32 bg-slate-200 rounded"></div>
      </div>
    );
  }

  return (
    <div className="h-16 border-b flex items-center justify-between px-4">
      <div className="flex items-center gap-3">
        <Avatar>
          <AvatarImage src={otherUser.avatar_url || ''} />
          <AvatarFallback>
            {otherUser.full_name?.charAt(0) || otherUser.username?.charAt(0) || '?'}
          </AvatarFallback>
        </Avatar>
        <div>
          <h2 className="font-medium">
            {otherUser.full_name || otherUser.username || 'User'}
          </h2>
          <p className="text-xs text-slate-500">
            {otherUser.username && `@${otherUser.username}`}
          </p>
        </div>
      </div>
      <DropdownMenu>
        <DropdownMenuTrigger asChild>
          <button className="h-8 w-8 rounded-full flex items-center justify-center hover:bg-slate-100">
            <MoreVertical className="h-5 w-5" />
          </button>
        </DropdownMenuTrigger>
        <DropdownMenuContent align="end">
          <DropdownMenuLabel>Actions</DropdownMenuLabel>
          <DropdownMenuSeparator />
          <DropdownMenuItem>
            <Info className="mr-2 h-4 w-4" />
            <span>View Profile</span>
          </DropdownMenuItem>
        </DropdownMenuContent>
      </DropdownMenu>
    </div>
  );
};
```

```tsx
// src/components/chat/chat-input.tsx
"use client";

import { Button } from "@/components/ui/button";
import { Form, FormControl, FormField, FormItem } from "@/components/ui/form";
import { Input } from "@/components/ui/input";
import { Send } from "lucide-react";
import { zodResolver } from "@hookform/resolvers/zod";
import { useForm } from "react-hook-form";
import { z } from "zod";
import { useEffect, useRef } from "react";

const formSchema = z.object({
  message: z.string().min(1),
});

interface ChatInputProps {
  onSend: (message: string) => void;
  isDisabled?: boolean;
}

export const ChatInput = ({ onSend, isDisabled }: ChatInputProps) => {
  const inputRef = useRef<HTMLInputElement>(null);
  
  const form = useForm<z.infer<typeof formSchema>>({
    resolver: zodResolver(formSchema),
    defaultValues: {
      message: "",
    },
  });

  const isSubmitting = form.formState.isSubmitting;

  const handleSubmit = async (values: z.infer<typeof formSchema>) => {
    onSend(values.message);
    form.reset();
  };

  // Focus the input when component mounts
  useEffect(() => {
    if (inputRef.current) {
      inputRef.current.focus();
    }
  }, []);

  return (
    <div className="p-4 border-t">
      <Form {...form}>
        <form onSubmit={form.handleSubmit(handleSubmit)} className="flex gap-2">
          <FormField
            control={form.control}
            name="message"
            render={({ field }) => (
              <FormItem className="flex-1">
                <FormControl>
                  <Input
                    {...field}
                    ref={inputRef}
                    placeholder="Type a message..."
                    disabled={isSubmitting || isDisabled}
                    className="focus-visible:ring-0 focus-visible:ring-offset-0"
                  />
                </FormControl>
              </FormItem>
            )}
          />
          <Button
            size="icon"
            disabled={isSubmitting || isDisabled}
            type="submit"
          >
            <Send className="h-5 w-5" />
          </Button>
        </form>
      </Form>
    </div>
  );
};
```

```tsx
// src/components/chat/message-item.tsx
"use client";

import { MessageWithSender, GroupMessageWithSender } from "@/types/supabase";
import { cn } from "@/lib/utils";
import { Avatar, AvatarFallback, AvatarImage } from "@/components/ui/avatar";
import { useUser } from "@clerk/nextjs";
import { format } from "date-fns";

interface MessageItemProps {
  message: MessageWithSender | GroupMessageWithSender;
  isGroupChat?: boolean;
}

export const MessageItem = ({ message, isGroupChat }: MessageItemProps) => {
  const { user } = useUser();

  const isOwn = user?.id === message.sender.clerk_id;
  
  return (
    <div className={cn(
      "flex gap-2 mb-4",
      isOwn && "justify-end"
    )}>
      {!isOwn && (
        <Avatar className="h-8 w-8">
          <AvatarImage src={message.sender.avatar_url || ''} />
          <AvatarFallback>
            {message.sender.full_name?.charAt(0) || 
             message.sender.username?.charAt(0) || 
             '?'}
          </AvatarFallback>
        </Avatar>
      )}
      <div className={cn(
        "flex flex-col max-w-[70%]",
        isOwn && "items-end"
      )}>
        {(!isOwn && isGroupChat) && (
          <p className="text-xs text-slate-500 mb-1">
            {message.sender.username || message.sender.full_name}
          </p>
        )}
        <div className={cn(
          "rounded-lg px-3 py-2",
          isOwn 
            ? "bg-blue-600 text-white rounded-tr-none" 
            : "bg-slate-200 rounded-tl-none"
        )}>
          <p className="text-sm">{message.content}</p>
        </div>
        <span className="text-xs text-slate-500 mt-1">
          {format(new Date(message.created_at), 'HH:mm')}
        </span>
      </div>
      {isOwn && (
        <Avatar className="h-8 w-8">
          <AvatarImage src={user?.imageUrl} />
          <AvatarFallback>
            {user?.firstName?.charAt(0) || 
             user?.username?.charAt(0) || 
             '?'}
          </AvatarFallback>
        </Avatar>
      )}
    </div>
  );
};
```

```tsx
// src/components/chat/chat-messages.tsx
"use client";

import { useEffect, useRef } from "react";
import { MessageWithSender, GroupMessageWithSender } from "@/types/supabase";
import { MessageItem } from "./message-item";

interface ChatMessagesProps {
  messages: MessageWithSender[] | GroupMessageWithSender[];
  isLoading: boolean;
  isGroupChat?: boolean;
}

export const ChatMessages = ({ 
  messages, 
  isLoading,
  isGroupChat = false
}: ChatMessagesProps) => {
  const scrollRef = useRef<HTMLDivElement>(null);

  // Scroll to bottom when messages change
  useEffect(() => {
    if (scrollRef.current) {
      scrollRef.current.scrollTop = scrollRef.current.scrollHeight;
    }
  }, [messages]);

  if (isLoading) {
    return (
      <div className="flex-1 p-4 overflow-y-auto">
        <div className="space-y-4">
          {[1, 2, 3].map((i) => (
            <div key={i} className="flex items-start gap-2">
              <div className="h-8 w-8 rounded-full bg-slate-200" />
              <div className="space-y-2">
                <div className="h-4 w-20 bg-slate-200 rounded" />
                <div className="h-10 w-64 bg-slate-200 rounded-lg" />
              </div>
            </div>
          ))}
        </div>
      </div>
    );
  }

  if (messages.length === 0) {
    return (
      <div className="flex-1 flex items-center justify-center p-4">
        <div className="text-center text-slate-500">
          <p>No messages yet</p>
          <p className="text-sm">Send a message to start the conversation</p>
        </div>
      </div>
    );
  }

  return (
    <div ref={scrollRef} className="flex-1 p-4 overflow-y-auto">
      <div className="space-y-4">
        {messages.map((message) => (
          <MessageItem 
            key={message.id} 
            message={message} 
            isGroupChat={isGroupChat}
          />
        ))}
      </div>
    </div>
  );
};
```

For group chat components:

```tsx
// src/components/groups/group-header.tsx
"use client";

import { Group, Profile } from "@/types/supabase";
import { Avatar, AvatarFallback, AvatarImage } from "@/components/ui/avatar";
import { Info, MoreVertical, Users } from "lucide-react";
import {
  DropdownMenu,
  DropdownMenuContent,
  DropdownMenuItem,
  DropdownMenuLabel,
  DropdownMenuSeparator,
  DropdownMenuTrigger,
} from "@/components/ui/dropdown-menu";

interface GroupHeaderProps {
  group: Group;
  memberCount: number;
  onViewMembers: () => void;
}

export const GroupHeader = ({ group, memberCount, onViewMembers }: GroupHeaderProps) => {
  return (
    <div className="h-16 border-b flex items-center justify-between px-4">
      <div className="flex items-center gap-3">
        <Avatar>
          <AvatarImage src={group.avatar_url || ''} />
          <AvatarFallback>
            {group.name.charAt(0) || 'G'}
          </AvatarFallback>
        </Avatar>
        <div>
          <h2 className="font-medium">{group.name}</h2>
          <p className="text-xs text-slate-500">
            {memberCount} {memberCount === 1 ? 'member' : 'members'}
          </p>
        </div>
      </div>
      <DropdownMenu>
        <DropdownMenuTrigger asChild>
          <button className="h-8 w-8 rounded-full flex items-center justify-center hover:bg-slate-100">
            <MoreVertical className="h-5 w-5" />
          </button>
        </DropdownMenuTrigger>
        <DropdownMenuContent align="end">
          <DropdownMenuLabel>Group Actions</DropdownMenuLabel>
          <DropdownMenuSeparator />
          <DropdownMenuItem onClick={onViewMembers}>
            <Users className="mr-2 h-4 w-4" />
            <span>View Members</span>
          </DropdownMenuItem>
          <DropdownMenuItem>
            <Info className="mr-2 h-4 w-4" />
            <span>Group Info</span>
          </DropdownMenuItem>
        </DropdownMenuContent>
      </DropdownMenu>
    </div>
  );
};
```

```tsx
// src/components/groups/group-members.tsx
"use client";

import { Profile } from "@/types/supabase";
import { Dialog, DialogContent, DialogHeader, DialogTitle } from "@/components/ui/dialog";
import { Avatar, AvatarFallback, AvatarImage } from "@/components/ui/avatar";
import { ScrollArea } from "@/components/ui/scroll-area";

interface GroupMembersProps {
  members: (Profile & { role: string })[];
  isOpen: boolean;
  onClose: () => void;
}

export const GroupMembers = ({ members, isOpen, onClose }: GroupMembersProps) => {
  return (
    <Dialog open={isOpen} onOpenChange={onClose}>
      <DialogContent className="sm:max-w-md">
        <DialogHeader>
          <DialogTitle>Group Members</DialogTitle>
        </DialogHeader>
        <ScrollArea className="mt-2 max-h-[60vh]">
          <div className="space-y-4 p-2">
            {members.map((member) => (
              <div key={member.id} className="flex items-center justify-between">
                <div className="flex items-center gap-3">
                  <Avatar>
                    <AvatarImage src={member.avatar_url || ''} />
                    <AvatarFallback>
                      {member.full_name?.charAt(0) || member.username?.charAt(0) || '?'}
                    </AvatarFallback>
                  </Avatar>
                  <div>
                    <p className="font-medium">
                      {member.full_name || member.username || 'User'}
                    </p>
                    <p className="text-xs text-slate-500">
                      @{member.username || 'user'}
                    </p>
                  </div>
                </div>
                {member.role === 'admin' && (
                  <span className="text-xs bg-slate-100 px-2 py-1 rounded">
                    Admin
                  </span>
                )}
              </div>
            ))}
          </div>
        </ScrollArea>
      </DialogContent>
    </Dialog>
  );
};
```

```tsx
// src/components/groups/create-group-form.tsx
"use client";

import { zodResolver } from "@hookform/resolvers/zod";
import { useForm } from "react-hook-form";
import { z } from "zod";
import { Button } from "@/components/ui/button";
import {
  Dialog,
  DialogContent,
  DialogHeader,
  DialogTitle,
  DialogTrigger,
} from "@/components/ui/dialog";
import {
  Form,
  FormControl,
  FormField,
  FormItem,
  FormLabel,
  FormMessage,
} from "@/components/ui/form";
import { Input } from "@/components/ui/input";
import { Textarea } from "@/components/ui/textarea";
import { useUser } from "@clerk/nextjs";
import { useSupabase } from "@/components/providers/supabase-provider";
import { useRouter } from "next/navigation";
import { Plus } from "lucide-react";
import { useState } from "react";
import { toast } from "react-hot-toast";

const formSchema = z.object({
  name: z.string().min(1, "Group name is required"),
  description: z.string().optional(),
});

export const CreateGroupForm = () => {
  const { user } = useUser();
  const { supabase } = useSupabase();
  const router = useRouter();
  const [open, setOpen] = useState(false);
  
  const form = useForm<z.infer<typeof formSchema>>({
    resolver: zodResolver(formSchema),
    defaultValues: {
      name: "",
      description: "",
    },
  });

  const onSubmit = async (values: z.infer<typeof formSchema>) => {
    if (!user?.id) return;
    
    try {
      // Get current user's profile
      const { data: myProfile } = await supabase
        .from('profiles')
        .select('*')
        .eq('clerk_id', user.id)
        .single();
      
      if (!myProfile) {
        throw new Error("User profile not found");
      }
      
      // Create the group
      const { data: group, error } = await supabase
        .from('groups')
        .insert({
          name: values.name,
          description: values.description,
          created_by: myProfile.id,
        })
        .select('*')
        .single();
      
      if (error) throw error;
      
      // Add creator as admin
      await supabase
        .from('group_members')
        .insert({
          group_id: group.id,
          user_id: myProfile.id,
          role: 'admin',
        });
      
      toast.success("Group created successfully");
      router.push(`/groups/${group.id}`);
      setOpen(false);
      form.reset();
    } catch (error) {
      console.error("Error creating group:", error);
      toast.error("Failed to create group");
    }
  };

  return (
    <Dialog open={open} onOpenChange={setOpen}>
      <DialogTrigger asChild>
        <Button size="sm" className="gap-1">
          <Plus className="h-4 w-4" />
          New Group
        </Button>
      </DialogTrigger>
      <DialogContent>
        <DialogHeader>
          <DialogTitle>Create New Group</DialogTitle>
        </DialogHeader>
        <Form {...form}>
          <form onSubmit={form.handleSubmit(onSubmit)} className="space-y-4 mt-2">
            <FormField
              control={form.control}
              name="name"
              render={({ field }) => (
                <FormItem>
                  <FormLabel>Group Name</FormLabel>
                  <FormControl>
                    <Input placeholder="Enter group name" {...field} />
                  </FormControl>
                  <FormMessage />
                </FormItem>
              )}
            />
            <FormField
              control={form.control}
              name="description"
              render={({ field }) => (
                <FormItem>
                  <FormLabel>Description (Optional)</FormLabel>
                  <FormControl>
                    <Textarea 
                      placeholder="What's this group about?" 
                      {...field} 
                    />
                  </FormControl>
                  <FormMessage />
                </FormItem>
              )}
            />
            <div className="flex justify-end gap-2">
              <Button 
                variant="outline" 
                type="button" 
                onClick={() => setOpen(false)}
              >
                Cancel
              </Button>
              <Button type="submit">Create Group</Button>
            </div>
          </form>
        </Form>
      </DialogContent>
    </Dialog>
  );
};
```

## Routing & Pages

Now let's implement our main pages:

```tsx
// src/app/(dashboard)/chat/[chatId]/page.tsx
"use client";

import { useParams } from "next/navigation";
import { useChat } from "@/hooks/use-chat";
import { ChatHeader } from "@/components/chat/chat-header";
import { ChatMessages } from "@/components/chat/chat-messages";
import { ChatInput } from "@/components/chat/chat-input";

export default function ChatPage() {
  const params = useParams();
  const chatId = params.chatId as string;
  const { messages, loading, otherUser, sendMessage } = useChat(chatId);

  return (
    <div className="flex flex-col h-full">
      <ChatHeader otherUser={otherUser} />
      <ChatMessages messages={messages} isLoading={loading} />
      <ChatInput onSend={sendMessage} isDisabled={loading} />
    </div>
  );
}
```

```tsx
// src/app/(dashboard)/groups/[groupId]/page.tsx
"use client";

import { useParams } from "next/navigation";
import { useGroup } from "@/hooks/use-groups";
import { GroupHeader } from "@/components/groups/group-header";
import { ChatMessages } from "@/components/chat/chat-messages";
import { ChatInput } from "@/components/chat/chat-input";
import { GroupMembers } from "@/components/groups/group-members";
import { useState } from "react";

export default function GroupPage() {
  const params = useParams();
  const groupId = params.groupId as string;
  const { messages, members, groupName, loading, sendMessage } = useGroup(groupId);
  const [showMembers, setShowMembers] = useState(false);

  return (
    <div className="flex flex-col h-full">
      <GroupHeader 
        group={{ id: groupId, name: groupName, avatar_url: null }} 
        memberCount={members.length} 
        onViewMembers={() => setShowMembers(true)}
      />
      <ChatMessages 
        messages={messages} 
        isLoading={loading} 
        isGroupChat={true}
      />
      <ChatInput onSend={sendMessage} isDisabled={loading} />
      <GroupMembers 
        members={members} 
        isOpen={showMembers} 
        onClose={() => setShowMembers(false)}
      />
    </div>
  );
}
```

```tsx
// src/app/(dashboard)/groups/new/page.tsx
"use client";

import { CreateGroupForm } from "@/components/groups/create-group-form";
import { useRouter } from "next/navigation";
import { useEffect } from "react";

export default function NewGroupPage() {
  const router = useRouter();
  
  // This page is just a wrapper to show the dialog immediately
  useEffect(() => {
    // If user navigates away without creating a group, go back
    const handleBeforeUnload = () => {
      router.back();
    };
    
    window.addEventListener('beforeunload', handleBeforeUnload);
    return () => {
      window.removeEventListener('beforeunload', handleBeforeUnload);
    };
  }, [router]);
  
  return (
    <div className="flex items-center justify-center h-full">
      <CreateGroupForm />
    </div>
  );
}
```

```tsx
// src/app/(dashboard)/settings/page.tsx
"use client";

import { Button } from "@/components/ui/button";
import { useUser } from "@clerk/nextjs";
import { useSupabase } from "@/components/providers/supabase-provider";
import { useRouter } from "next/navigation";
import { Avatar, AvatarFallback, AvatarImage } from "@/components/ui/avatar";
import { toast } from "react-hot-toast";

export default function SettingsPage() {
  const { user } = useUser();
  const { supabase } = useSupabase();
  const router = useRouter();

  const handleDeleteAccount = async () => {
    if (!user?.id || !window.confirm("Are you sure you want to delete your account? This cannot be undone.")) {
      return;
    }

    try {
      // Get profile ID
      const { data: profile } = await supabase
        .from('profiles')
        .select('id')
        .eq('clerk_id', user.id)
        .single();

      if (!profile) {
        throw new Error("Profile not found");
      }

      // Delete all user data from Supabase
      await supabase.from('messages').delete().eq('sender_id', profile.id);
      await supabase.from('group_messages').delete().eq('sender_id', profile.id);
      await supabase.from('chat_participants').delete().eq('user_id', profile.id);
      await supabase.from('group_members').delete().eq('user_id', profile.id);
      await supabase.from('profiles').delete().eq('id', profile.id);

      // Delete user from Clerk
      await user.delete();

      toast.success("Account deleted successfully");
      router.push("/");
    } catch (error) {
      console.error("Error deleting account:", error);
      toast.error("Failed to delete account");
    }
  };

  return (
    <div className="p-6 max-w-2xl mx-auto">
      <h1 className="text-2xl font-bold mb-6">Account Settings</h1>
      
      <div className="space-y-6">
        <div className="flex items-center gap-4">
          <Avatar className="h-16 w-16">
            <AvatarImage src={user?.imageUrl} />
            <AvatarFallback>
              {user?.firstName?.charAt(0) || user?.username?.charAt(0) || '?'}
            </AvatarFallback>
          </Avatar>
          <div>
            <h2 className="font-medium">
              {user?.fullName || user?.username || 'User'}
            </h2>
            <p className="text-sm text-slate-500">
              {user?.primaryEmailAddress?.emailAddress}
            </p>
          </div>
        </div>
        
        <div className="space-y-4">
          <div>
            <h3 className="font-medium mb-2">Personal Information</h3>
            <div className="bg-slate-50 p-4 rounded-lg">
              <p className="text-sm">
                <span className="text-slate-500">Name:</span> {user?.fullName}
              </p>
              <p className="text-sm mt-1">
                <span className="text-slate-500">Username:</span> @{user?.username}
              </p>
            </div>
          </div>
          
          <div>
            <h3 className="font-medium mb-2">Danger Zone</h3>
            <div className="border border-red-200 bg-red-50 p-4 rounded-lg">
              <p className="text-sm text-red-800 mb-3">
                Deleting your account will remove all your data from our servers. This cannot be undone.
              </p>
              <Button 
                variant="destructive" 
                size="sm"
                onClick={handleDeleteAccount}
              >
                Delete Account
              </Button>
            </div>
          </div>
        </div>
      </div>
    </div>
  );
}
```

## API Routes

Let's implement our API routes for additional functionality:

```tsx
// src/app/api/webhooks/clerk/route.ts
import { Webhook } from "svix";
import { headers } from "next/headers";
import { WebhookEvent } from "@clerk/nextjs/server";
import { createServerClient } from "@/lib/supabase";
import { NextResponse } from "next/server";

export async function POST(req: Request) {
  const WEBHOOK_SECRET = process.env.CLERK_WEBHOOK_SECRET;

  if (!WEBHOOK_SECRET) {
    throw new Error(
      "Please add CLERK_WEBHOOK_SECRET from Clerk Dashboard to .env"
    );
  }

  const headerPayload = headers();
  const svix_id = headerPayload.get("svix-id");
  const svix_timestamp = headerPayload.get("svix-timestamp");
  const svix_signature = headerPayload.get("svix-signature");

  if (!svix_id || !svix_timestamp || !svix_signature) {
    return new Response("Error occurred -- no svix headers", {
      status: 400,
    });
  }

  const payload = await req.json();
  const body = JSON.stringify(payload);

  const wh = new Webhook(WEBHOOK_SECRET);

  let evt: WebhookEvent;

  try {
    evt = wh.verify(body, {
      "svix-id": svix_id,
      "svix-timestamp": svix_timestamp,
      "svix-signature": svix_signature,
    }) as WebhookEvent;
  } catch (err) {
    console.error("Error verifying webhook:", err);
    return new Response("Error occurred", {
      status: 400,
    });
  }

  const supabase = createServerClient();
  const { id, first_name, last_name, username, image_url } = evt.data;

  try {
    switch (evt.type) {
      case "user.created":
        // Create profile in Supabase
        await supabase.from("profiles").insert({
          id: crypto.randomUUID(),
          clerk_id: id,
          username: username || null,
          full_name: `${first_name} ${last_name || ""}`.trim(),
          avatar_url: image_url,
        });
        break;

      case "user.updated":
        // Update profile in Supabase
        await supabase
          .from("profiles")
          .update({
            username: username || null,
            full_name: `${first_name} ${last_name || ""}`.trim(),
            avatar_url: image_url,
            updated_at: new Date().toISOString(),
          })
          .eq("clerk_id", id);
        break;

      case "user.deleted":
        // Delete profile from Supabase
        await supabase.from("profiles").delete().eq("clerk_id", id);
        break;
    }
  } catch (error) {
    console.error("Error handling webhook event:", error);
    return NextResponse.json(
      { error: "Internal server error" },
      { status: 500 }
    );
  }

  return NextResponse.json({ received: true }, { status: 200 });
}
```

## Extra Utilities

Let's add some utility functions:

```tsx
// src/lib/utils.ts
import { format } from "date-fns";

export function cn(...inputs: (string | boolean | undefined)[]) {
  return inputs.filter(Boolean).join(" ");
}

export function formatDate(date: string | Date) {
  return format(new Date(date), "MMM d, yyyy");
}

export function formatTime(date: string | Date) {
  return format(new Date(date), "h:mm a");
}

export function formatDateTime(date: string | Date) {
  return format(new Date(date), "MMM d, yyyy 'at' h:mm a");
}

export function truncate(str: string, length: number) {
  return str.length > length ? `${str.substring(0, length)}...` : str;
}

export function getInitials(name?: string | null) {
  if (!name) return "?";

  const parts = name.split(" ");
  if (parts.length === 1) return parts[0].charAt(0).toUpperCase();

  return `${parts[0].charAt(0)}${parts[parts.length - 1].charAt(0)}`.toUpperCase();
}
```

## Tips & Optimization

Here are some final tips and optimization suggestions:

1. **Performance Optimization**:
   - Use React's `useMemo` and `useCallback` hooks to prevent unnecessary re-renders
   - Implement pagination for chat messages to load messages in chunks
   - Use Next.js's `dynamic` imports for heavy components

2. **Security Best Practices**:
   - Always validate user input on both client and server
   - Use Row Level Security (RLS) in Supabase for all tables
   - Implement rate limiting on API routes
   - Store sensitive environment variables securely

3. **Deployment Notes**:
   - Set up proper CORS policies for your Supabase instance
   - Configure Clerk's webhook in production to point to your live URL
   - Use a CDN for static assets
   - Implement proper error logging and monitoring

4. **Additional Features**:
   - Add message reactions and replies
   - Implement file uploads and media sharing
   - Add typing indicators
   - Implement message search functionality
   - Add dark mode support

5. **Testing**:
   - Write unit tests for utility functions
   - Implement end-to-end tests for critical user flows
   - Test the application on different screen sizes

To deploy your application:

```bash
# Build the application
npm run build

# Start the production server
npm run start
```

For production deployment, consider using:
- Vercel (recommended for Next.js)
- Netlify
- AWS Amplify
- Docker containers on your preferred cloud provider

This completes our comprehensive real-time chat application implementation with Next.js 15, Clerk authentication, Supabase for real-time data, and ShadcnUI for components. The application includes:

- Secure authentication with Clerk
- 1-on-1 and group messaging
- Real-time updates via Supabase channels
- Responsive UI with Tailwind CSS
- Clean, modular code structure
- TypeScript support throughout
- Proper error handling and loading states
- User settings and account management

The application follows best practices for modern web development and provides a solid foundation for further customization and feature additions.
