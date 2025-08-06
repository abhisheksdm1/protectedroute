
````
import React from "react";
import { Navigate, Outlet } from "react-router-dom";

const ProtectedRoute = ({ allowedRole }) => {
  const { role } = JSON.parse(localStorage.getItem("MERCHANT_DATA"));

  if (!role) {
    return <Navigate to="/" />;
  }

  if (role !== allowedRole) {
    return (
      <div className="text-red-500 text-center mt-4">
        Access Denied — Current role: . Required: .
      </div>
    );
  }

  return <Outlet />;
};

export default ProtectedRoute;

````
