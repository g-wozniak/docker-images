RUN pwd

RUN git clone -b adjusting_tests --single-branch https://github.com/g-wozniak/cv2.git

WORKDIR /app/cv2

RUN npm ci

RUN npm run test:ci:webapp

#RUN npm run build