#                               Next js

import { NextRequest, NextResponse } from 'next/server';

export function middleware(request: NextRequest) {
    // Example: Redirect if user is not authenticated
    const isAuthenticated = request.cookies.get('auth_token');

    if (!isAuthenticated) {
        return NextResponse.redirect(new URL('/login', request.url));
    }

    return NextResponse.next();
}

// Apply middleware only to specific routes
export const config = {
    matcher: ['/dashboard/:path*', '/admin/:path*'], // Middleware runs only for these paths
};
    remove config if apply 