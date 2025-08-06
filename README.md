
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

##APP.jsx

````
import {
  BrowserRouter,
  createBrowserRouter,
  RouterProvider,
  useNavigate,
} from "react-router-dom";
import Dashboard from "./Components/Dashboard";
import "./App.css";
import HomePage from "./HomePage";
import CampaignDashboard from "./Promotion/CampaignDashboard";
import AnalyticsInsights from "./Analytics/AnalyticsInsights";
import GamificationDashboard from "./Gamification/GamificationDashboard";
import AhadLogin from "./OnBoarding/AhadLogin";
import StaffManagement from "./Staff/StaffManangment";
import OpenSettings from "./Settiongs/OpenSettings";
import CreateMasterDashboard from "./Masters/AllMastertabs";
import CreateCampign from "./Promotion/CampignForm";
import CampainIndividual from "./Promotion/CampainIndividual";
import StampPromotion from "./Stamp/StampPromotion";
import GameMasterForm from "./Gamification/GameMasterForm";
import StampDashboard from "./Stamp/StampDashboard";
import SupportDashboard from "./Supports/SupportDashboard";
import CreateTicketForm from "./Supports/CreateTicketForm";
import Register from "./OnBoarding/Register";
import LeadManagement from "./Lead/LeadManagement";
import MerchantManagement from "./Merchant/MerchantManagement";
import RestPasswordLogin from "./OnBoarding/RestPasswordLogin";
import BuisnessInformation from "./KYB/BuisnessInformation";
import ApprovalCentralDashboard from "./ApprovalCentral/ApprovalCentralDashboard";
import PointsandTransactions from "./PointsandTrans/PoinstandTransaction";
import CustomerProfile from "./Customer/CustomerProfile";
import CustomerTable from "./Customer/CustomerTable";
import ProtectedRoute from "./Components/ProtectedRoute";
const router = createBrowserRouter([
  {
    path: "/login",
    element: <AhadLogin />,
  },
  {
    path: "/merchant-login",
    element: <RestPasswordLogin />,
  },
  {
    path: "/register",
    element: <Register />,
  },
  {
    path: "/kyb",
    element: <BuisnessInformation />,
  },
  {
    path: "/",
    element: <HomePage />,
    errorElement: <Error />,
    children: [
      {
        index: true,
        element: <Dashboard />,
      },
      {
        path: "lead-management",
        element: <ProtectedRoute allowedRole="ADMIN" />,
        children: [{ index: true, element: <LeadManagement /> }],
      },
      {
        path: "merchant-management",
        element: <ProtectedRoute allowedRole="ADMIN" />,
        children: [{ index: true, element: <MerchantManagement /> }],
      },
      {
        path: "approval-central",
        element: <ProtectedRoute allowedRole="ADMIN" />,
        children: [{ index: true, element: <ApprovalCentralDashboard /> }],
      },
      {
        path: "masters",
        element: <CreateMasterDashboard />,
      },
      {
        path: "customer",
        element: <ProtectedRoute allowedRole="ADMIN" />,
        children: [{ index: true, element: <CustomerTable /> }],
      },
      {
        path: "customer-profile",
        element: <ProtectedRoute allowedRole="ADMIN" />,
        children: [{ index: true, element: <CustomerProfile /> }],
      },
      {
        path: "point-transactions",
        element: <ProtectedRoute allowedRole="ADMIN" />,
        children: [{ index: true, element: <PointsandTransactions /> }],
      },
      {
        path: "analytics",
        element: <ProtectedRoute allowedRole="ADMIN" />,
        children: [{ index: true, element: <AnalyticsInsights /> }],
      },
      {
        path: "promotion",
        element: <ProtectedRoute allowedRole="ADMIN" />,
        children: [{ index: true, element: <CampaignDashboard /> }],
      },
      {
        path: "promotion/create",
        element: <ProtectedRoute allowedRole="ADMIN" />,
        children: [{ index: true, element: <CreateCampign /> }],
      },
      {
        path: "supports",
        element: <ProtectedRoute allowedRole="ADMIN" />,
        children: [{ index: true, element: <SupportDashboard /> }],
      },
      {
        path: "supports/create",
        element: <ProtectedRoute allowedRole="ADMIN" />,
        children: [{ index: true, element: <CreateTicketForm /> }],
      },
      {
        path: "stamp",
        element: <ProtectedRoute allowedRole="ADMIN" />,
        children: [{ index: true, element: <StampDashboard /> }],
      },
      {
        path: "stamp/create",
        element: <ProtectedRoute allowedRole="ADMIN" />,
        children: [{ index: true, element: <StampPromotion /> }],
      },
      {
        path: "promotion/update/:id",
        element: <ProtectedRoute allowedRole="ADMIN" />,
        children: [{ index: true, element: <CreateCampign /> }],
      },
      {
        path: "promotion/:id",
        element: <ProtectedRoute allowedRole="ADMIN" />,
        children: [{ index: true, element: <CampainIndividual /> }],
      },
      {
        path: "gamification",
        element: <ProtectedRoute allowedRole="ADMIN" />,
        children: [{ index: true, element: <GamificationDashboard /> }],
      },
      {
        path: "gamification/create",
        element: <ProtectedRoute allowedRole="ADMIN" />,
        children: [{ index: true, element: <GameMasterForm /> }],
      },
      {
        path: "staff",
        element: <ProtectedRoute allowedRole="ADMIN" />,
        children: [{ index: true, element: <StaffManagement /> }],
      },
      {
        path: "settings",
        element: <ProtectedRoute allowedRole="ADMIN" />,
        children: [{ index: true, element: <OpenSettings /> }],
      },
    ],
  },
]);

function App() {
  return <RouterProvider router={router} />;
}

export default App;
````
