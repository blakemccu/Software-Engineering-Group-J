# MösFit API Documentation

## 🌍 Base URL
`https://api.mosfit.com/v1`

## 🔑 Authentication Endpoints
| Method | Endpoint        | Description |
|--------|----------------|-------------|
| POST   | `/auth/register` | Register a new user |
| POST   | `/auth/login`    | Authenticate user & return JWT |
| GET    | `/auth/profile`  | Get user profile info |

## 🏋️ Workout Endpoints
| Method | Endpoint          | Description |
|--------|------------------|-------------|
| GET    | `/workouts`       | Get all workouts for the user |
| POST   | `/workouts`       | Log a new workout |
| GET    | `/workouts/{id}`  | Get workout details by ID |
| DELETE | `/workouts/{id}`  | Delete a specific workout |

## 🍎 Nutrition Endpoints
| Method | Endpoint          | Description |
|--------|------------------|-------------|
| GET    | `/nutrition/logs`  | Retrieve meal logs |
| POST   | `/nutrition/logs`  | Add a new meal |
| DELETE | `/nutrition/{id}`  | Delete a meal entry |

## 📊 Progress Tracking Endpoints
| Method | Endpoint           | Description |
|--------|-------------------|-------------|
| GET    | `/progress`        | Get user progress metrics |
| GET    | `/progress/weekly` | Get weekly progress summary |

---

## 🔄 How to Use This API
1. **Authentication Required:** Most endpoints need a valid JWT token.
2. **Base URL:** Use `https://api.mosfit.com/v1` for requests.
3. **Data Format:** Requests & responses are in JSON.

---

## 📌 Notes
- If you encounter issues, contact support at `support@mosfit.com`
- API rate limits: **60 requests per minute**
