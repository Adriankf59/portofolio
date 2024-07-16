FROM node:18-alpine AS base

# Step 2. Production image, copy all the files and run next
FROM base AS runner
WORKDIR /app
ENV NODE_ENV production

# Don't run production as root
RUN addgroup --system --gid 1001 nodejs
RUN adduser --system --uid 1001 nextjs
USER nextjs

COPY ./public ./public

# Automatically leverage output traces to reduce image size
# https://nextjs.org/docs/advanced-features/output-file-tracing
COPY --chown=nextjs:nodejs .next/standalone ./
COPY --chown=nextjs:nodejs .next/static  ./.next/static

# Environment variables must be redefined at run time
# ARG NEXT_PUBLIC_BASE_URL
# ENV NEXT_PUBLIC_BASE_URL=${NEXT_PUBLIC_BASE_URL}

# ARG NEXT_PUBLIC_ENV_VARIABLE
# ENV NEXT_PUBLIC_ENV_VARIABLE=${NEXT_PUBLIC_ENV_VARIABLE}

# Uncomment the following line to disable telemetry at run time
# ENV NEXT_TELEMETRY_DISABLED 1

# Note: Don't expose ports here, Compose will handle that for us

CMD ["node", "server.js"]