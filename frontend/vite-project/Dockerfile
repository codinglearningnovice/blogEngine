
FROM node:20-alpine


WORKDIR /app


COPY package*.json ./
RUN npm install


COPY . .

# 5. Vite's default port
EXPOSE 5173


#  use --host to make sure it's accessible outside the container
CMD ["npm", "run", "dev", "--", "--host"]