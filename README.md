using NEWAIHR_API.ViewModel;
using NEWAIHR.Models;
using System.Net;
using System.Net.Http;
using System.Linq;
using System.Text;
using Newtonsoft.Json.Linq;
using System;
using System.Web.Http;
using NEWAIHR.ViewModel;

namespace NEWAIHR.Controllers
{
    public class ValuesController : ApiController
    {
        NewAIHREntities db = new NewAIHREntities();

        #region ==> OWNER 
        public HttpResponseMessage OwnerGet(UserModel PMM)
        {
            try
            {
                var re = db.BDL_OwnerRtr(PMM.ActionD , PMM.OwnerMainID).ToList();
                var response = Request.CreateResponse(HttpStatusCode.OK, re);
                return response;
            }
            catch (Exception ex)
            {
                var response = Request.CreateResponse(HttpStatusCode.BadRequest, ex);
                string query3 = "{ \"Result \":\"Data Not Fetch\"}";
                var jObject = JObject.Parse(query3);
                response.Content = new StringContent(jObject.ToString(), Encoding.UTF8, "application/json");
                return response;
            }
            finally
            { db.Dispose(); }
        }
        public HttpResponseMessage OwnerAdd(UserModel pmm)
        {
            try
            {
                var re = db.BDL_OwnerInsUp(pmm.OwnerMainID, pmm.OwnerName, pmm.Gender,pmm.Address, pmm.MobileNo, pmm.Password, pmm.DOB, pmm.Caste, pmm.State, pmm.District, pmm.Taluka, pmm.UIDNo, pmm.LandHolding, pmm.MilchAnimals, pmm.CreateUser, pmm.CreateDate.ToString(), pmm.UpdateUser, pmm.UpdateDate.ToString(), pmm.ActionD).FirstOrDefault();
                var response = Request.CreateResponse(HttpStatusCode.OK, re);
                //string query3 = "{ \"Result \":\"Data Insert successfully\"}";
                //var jObject = JObject.Parse(query3);
                //response.Content = new StringContent(jObject.ToString(), Encoding.UTF8, "application/json");
                return response;
            }
            catch (Exception ex)
            {
                var response = Request.CreateResponse(HttpStatusCode.BadRequest, ex);
                return response;
            }
            finally
            { db.Dispose(); }
        }
        #endregion

        #region ==> Bread

        public HttpResponseMessage BreedGet(Breead1 PMM)
        {
            try
            {
                var re = db.BDL_BreadRtr(PMM.ActionD).ToList();
                var response = Request.CreateResponse(HttpStatusCode.OK, re);
                return response;
            }
            catch (Exception ex)
            {
                var response = Request.CreateResponse(HttpStatusCode.BadRequest, ex);
                string query3 = "{ \"Result \":\"Data Not Fetch\"}";
                var jObject = JObject.Parse(query3);
                response.Content = new StringContent(jObject.ToString(), Encoding.UTF8, "application/json");
                return response;
            }
            finally
            { db.Dispose(); }
        }
        public HttpResponseMessage BreedAdd(Breead1 pmm)
        {
            try
            {
                var re = db.BDL_BreadInsUp(pmm.BreedID.ToString(), pmm.BreedName, pmm.SpeciesID.ToString(), pmm.CreateUser, pmm.CreateDate, pmm.UpdateUser, pmm.UpdateDate, pmm.ActionD).FirstOrDefault();
                var response = Request.CreateResponse(HttpStatusCode.OK, re);
                string query3 = "{ \"Result \":\"Data Insert successfully\"}";
                var jObject = JObject.Parse(query3);
                response.Content = new StringContent(jObject.ToString(), Encoding.UTF8, "application/json");
                return response;
            }
            catch (Exception ex)
            {
                var response = Request.CreateResponse(HttpStatusCode.BadRequest, ex);
                return response;
            }
            finally
            { db.Dispose(); }
        }

        #endregion

        #region ==> Species Master 

        public HttpResponseMessage SpeciesMasterGet(UserModel lc)
        {
            try
            {
                var re = db.BDL_SpeciesMasterRtr("All").ToList();
                var response = Request.CreateResponse(HttpStatusCode.OK, re);
                return response;
            }
            catch (Exception ex)
            {
                var response = Request.CreateResponse(HttpStatusCode.BadRequest, ex);
                string query3 = "{ \"Result \":\"Data Not Fetch\"}";
                var jObject = JObject.Parse(query3);
                response.Content = new StringContent(jObject.ToString(), Encoding.UTF8, "application/json");
                return response;
            }
            finally
            { db.Dispose(); }
        }

        public HttpResponseMessage SpeciesMasterAdd(Species pmm)
        {
            try
            {
                var re = db.BDL_SpeciesMasterInsUpd(pmm.SpeciesID.ToString(), pmm.SpeciesName, pmm.Isactive, pmm.CreateUser, pmm.CreateDate, pmm.UpdateUser, pmm.UpdateDate, pmm.ActionD).FirstOrDefault();
                var response = Request.CreateResponse(HttpStatusCode.OK, re);
                string query3 = "{ \"Result \":\"Species Name Insert successfully\"}";
                var jObject = JObject.Parse(query3);
                response.Content = new StringContent(jObject.ToString(), Encoding.UTF8, "application/json");
                return response;
            }
            catch (Exception ex)
            {
                var response = Request.CreateResponse(HttpStatusCode.BadRequest, ex);
                return response;
            }
            finally
            { db.Dispose(); }
        }

        #endregion

        #region ==> Visit Master GET API

        public HttpResponseMessage VisitMasterGet(UserModel lc)
        {
            try
            {
                var re = db.BDL_VisitMasterRtr("All").ToList();
                var response = Request.CreateResponse(HttpStatusCode.OK, re);
                return response;
            }
            catch (Exception ex)
            {
                var response = Request.CreateResponse(HttpStatusCode.BadRequest, ex);
                string query3 = "{ \"Result \":\"Data Not Fetch\"}";
                var jObject = JObject.Parse(query3);
                response.Content = new StringContent(jObject.ToString(), Encoding.UTF8, "application/json");
                return response;
            }
            finally
            { db.Dispose(); }
        }


        #endregion

        #region ==> Member API

        public HttpResponseMessage MemberGet(UserModel PMM)
        {
            try
            {
                var re = db.BDL_MemberRtr(PMM.ActionD, PMM.OwnerMainID).ToList();
                var response = Request.CreateResponse(HttpStatusCode.OK, re);
                return response;
            }
            catch (Exception ex)
            {
                var response = Request.CreateResponse(HttpStatusCode.BadRequest, ex);
                string query3 = "{ \"Result \":\"Data Not Fetch\"}";
                var jObject = JObject.Parse(query3);
                response.Content = new StringContent(jObject.ToString(), Encoding.UTF8, "application/json");
                return response;
            }
            finally 
            { db.Dispose(); }
        }
        public HttpResponseMessage MemberAdd(Member pmm)
        {
            try
            {
                var re = db.BDL_MemberInsUpd(pmm.MemberID, pmm.OwnerMainID, pmm.MemberName,pmm.Age, pmm.Gender,pmm.Address, pmm.MobileNo, pmm.DOB, pmm.State, pmm.District, pmm.Taluka, pmm.LandHolding, pmm.MilchAnimals, pmm.CreateUser, pmm.CreateDate, pmm.UpdateUser, pmm.UpdateDate, pmm.ActionD).FirstOrDefault();
                var response = Request.CreateResponse(HttpStatusCode.OK, re);
                string query3 = "{ \"Result \":\"Data Insert successfully\"}";
                var jObject = JObject.Parse(query3);
                response.Content = new StringContent(jObject.ToString(), Encoding.UTF8, "application/json");
                return response;
            }
            catch (Exception ex)
            {
                var response = Request.CreateResponse(HttpStatusCode.BadRequest, ex);
                return response;
            }
            finally
            { db.Dispose(); }
        }

        #endregion

        #region ==> Animal List 
        public HttpResponseMessage AnimalGet(AnimalList PMM)
        {
            try
            {
                var re = db.BDL_AnimalListRtr(PMM.ActionD, PMM.OwnerMainID, PMM.IsActive).ToList();
                var response = Request.CreateResponse(HttpStatusCode.OK, re);
                return response;
            }
            catch (Exception ex)
            {
                var response = Request.CreateResponse(HttpStatusCode.BadRequest, ex);
                string query3 = "{ \"Result \":\"Data Not Fetch\"}";
                var jObject = JObject.Parse(query3);
                response.Content = new StringContent(jObject.ToString(), Encoding.UTF8, "application/json");
                return response;
            }
            finally
            { db.Dispose(); }
        }

        public HttpResponseMessage AnimalAdd(AnimalList pmm)
        {
            try
            {
                var re = db.BDL_AnimalListInsUpd(pmm.AnimalID, pmm.TagID, pmm.OwnerMainID, pmm.MemberMainID, pmm.OwnerName, pmm.MemberName, pmm.Species, pmm.Breed, pmm.Gender, pmm.DOB, pmm.Age, pmm.Status, pmm.CreateUser, pmm.CreateDate.ToString(), pmm.UpdateUser, pmm.UpdateDate.ToString(),pmm.AnimalIsActive,pmm.ActionD).FirstOrDefault();
                var response = Request.CreateResponse(HttpStatusCode.OK, re);
                string query3 = "{ \"Result \":\"Data Insert successfully\"}";
                var jObject = JObject.Parse(query3);
                response.Content = new StringContent(jObject.ToString(), Encoding.UTF8, "application/json");
                return response;
            }
            catch (Exception ex)
            {
                var response = Request.CreateResponse(HttpStatusCode.BadRequest, ex);
                return response;
            }
            finally
            { db.Dispose(); }
        }
        #endregion

        #region ==> Ailment Master

        public HttpResponseMessage AilmentMasterGet(UserModel lc)
        {
            try
            {
                var re = db.BDL_AilmentMasterRtr("All").ToList();
                var response = Request.CreateResponse(HttpStatusCode.OK, re);
                return response;
            }
            catch (Exception ex)
            {
                var response = Request.CreateResponse(HttpStatusCode.BadRequest, ex);
                string query3 = "{ \"Result \":\"Data Not Fetch\"}";
                var jObject = JObject.Parse(query3);
                response.Content = new StringContent(jObject.ToString(), Encoding.UTF8, "application/json");
                return response;
            }
            finally
            { db.Dispose(); }
        }

        public HttpResponseMessage AilmentMasterAdd(AilmentMaster pmm)
        {
            try
            {
                var re = db.BDL_AilmentMasterInsUpd(pmm.AilmentID.ToString(), pmm.AilmentCode.ToString(), pmm.AilmentName, pmm.ActionD).FirstOrDefault();
                var response = Request.CreateResponse(HttpStatusCode.OK, re);
                string query3 = "{ \"Result \":\"Ailment Value Insert successfully\"}";
                var jObject = JObject.Parse(query3);
                response.Content = new StringContent(jObject.ToString(), Encoding.UTF8, "application/json");
                return response;
            }
            catch (Exception ex)
            {
                var response = Request.CreateResponse(HttpStatusCode.BadRequest, ex);
                return response;
            }
            finally
            { db.Dispose(); }
        }

        #endregion

        #region ==> Login API

        public HttpResponseMessage LoginCheck(Login pmm)
        {
            try
            {
                string re = db.BDL_LoginCheck(pmm.MobileNo, pmm.Password).ToString();
                if (re != null)
                {
                    var uc = db.BDL_LoginCheck(pmm.MobileNo, pmm.Password).FirstOrDefault();
                    var response2 = Request.CreateResponse(HttpStatusCode.OK, uc);
                    return response2;
                }
                else
                {
                    string query3 = "{ \"LoginResult\":\"Invalid Mobile No or Password\"}";
                    var jObject = JObject.Parse(query3);
                    var response = Request.CreateResponse(HttpStatusCode.OK);
                    response.Content = new StringContent(jObject.ToString(), Encoding.UTF8, "application/json");
                    return response;
                }
            }
            catch (Exception ex)
            {
                string query1 = "{ \"LoginResult\":\" Invalid Mobile No or Password \"}";
                var jObject = JObject.Parse(query1);
                var response = Request.CreateResponse(HttpStatusCode.BadRequest, ex);
                response.Content = new StringContent(jObject.ToString(), Encoding.UTF8, "application/json");
                return response;
            }
            finally
            { db.Dispose(); }
        }


        #endregion

        #region ==> Society Master API

        public HttpResponseMessage SocietyMasterGet(UserModel lc)
        {
            try
            {
                var re = db.BDL_SocietyMasterRtr("All").ToList();
                var response = Request.CreateResponse(HttpStatusCode.OK, re);
                return response;
            }
            catch (Exception ex)
            {
                var response = Request.CreateResponse(HttpStatusCode.BadRequest, ex);
                string query3 = "{ \"Result \":\"Data Not Fetch\"}";
                var jObject = JObject.Parse(query3);
                response.Content = new StringContent(jObject.ToString(), Encoding.UTF8, "application/json");
                return response;
            }
            finally
            { db.Dispose(); }
        }

        public HttpResponseMessage SocietyMasterAdd(SocietyMaster pmm)
        {
            try
            {
                var re = db.BDL_SocietyMasterInsUpd(pmm.SocietyID.ToString(), pmm.SocietyName, pmm.AreaID, pmm.ActionD).FirstOrDefault();
                var response = Request.CreateResponse(HttpStatusCode.OK, re);
                string query3 = "{ \"Result \":\"Society Name Insert successfully\"}";
                var jObject = JObject.Parse(query3);
                response.Content = new StringContent(jObject.ToString(), Encoding.UTF8, "application/json");
                return response;
            }
            catch (Exception ex)
            {
                var response = Request.CreateResponse(HttpStatusCode.BadRequest, ex);
                return response;
            }
            finally
            { db.Dispose(); }
        }

        #endregion

        #region ==> Area Master API

        public HttpResponseMessage AreaMasterGet(UserModel lc)
        {
            try
            {
                var re = db.BDL_AreaMasterRtr("All").ToList();
                var response = Request.CreateResponse(HttpStatusCode.OK, re);
                return response;
            }
            catch (Exception ex)
            {
                var response = Request.CreateResponse(HttpStatusCode.BadRequest, ex);
                string query3 = "{ \"Result \":\"Data Not Fetch\"}";
                var jObject = JObject.Parse(query3);
                response.Content = new StringContent(jObject.ToString(), Encoding.UTF8, "application/json");
                return response;
            }
            finally
            { db.Dispose(); }
        }

        public HttpResponseMessage AreaMasterAdd(AreaMaster pmm)
        {
            try
            {
                var re = db.BDL_AreaMasterInsUpd(pmm.AreaID.ToString(), pmm.AreaName, pmm.ActionD).FirstOrDefault();
                var response = Request.CreateResponse(HttpStatusCode.OK, re);
                string query3 = "{ \"Result \":\"Area Name Insert successfully\"}";
                var jObject = JObject.Parse(query3);
                response.Content = new StringContent(jObject.ToString(), Encoding.UTF8, "application/json");
                return response;
            }
            catch (Exception ex)
            {
                var response = Request.CreateResponse(HttpStatusCode.BadRequest, ex);
                return response;
            }
            finally
            { db.Dispose(); }
        }

        #endregion

        #region ==> Call Booking API

        public HttpResponseMessage CallBookingGet(UserModel lc)
        {
            try
            {
                var re = db.BDL_CallBookingRtr("All").ToList();
                var response = Request.CreateResponse(HttpStatusCode.OK, re);
                return response;
            }
            catch (Exception ex)
            {
                var response = Request.CreateResponse(HttpStatusCode.BadRequest, ex);
                string query3 = "{ \"Result \":\"Data Not Fetch\"}";
                var jObject = JObject.Parse(query3);
                response.Content = new StringContent(jObject.ToString(), Encoding.UTF8, "application/json");
                return response;
            }
            finally
            { db.Dispose(); }
        }
        public HttpResponseMessage CallBookingAdd(CallBooking pmm)
        {
            try
            {
                var re = db.BDL_CallBookingInsUpd(pmm.BookingID, pmm.OwnerMainID, pmm.MemberMainID, pmm.SocietyID.ToString(), pmm.VisitType, pmm.AnimalMainID, pmm.AilmentID.ToString(), pmm.Remark, pmm.ActionD).FirstOrDefault();
                var response = Request.CreateResponse(HttpStatusCode.OK, re);
                string query3 = "{ \"Result \":\"Call Booking Insert successfully\"}";
                var jObject = JObject.Parse(query3);
                response.Content = new StringContent(jObject.ToString(), Encoding.UTF8, "application/json");
                return response;
            }
            catch (Exception ex)
            {
                var response = Request.CreateResponse(HttpStatusCode.BadRequest, ex);
                return response;
            }
            finally
            { db.Dispose(); }
        }
        #endregion

        /////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

        #region Center Master

        public HttpResponseMessage CenterMasterGet(UserModel lc)
        {
            try
            {
                var re = db.BDL_CenterMasterRtr("All").ToList();
                var response = Request.CreateResponse(HttpStatusCode.OK, re);
                return response;
            }
            catch (Exception ex)
            {
                var response = Request.CreateResponse(HttpStatusCode.BadRequest, ex);
                string query3 = "{ \"Result \":\"Data Not Fetch\"}";
                var jObject = JObject.Parse(query3);
                response.Content = new StringContent(jObject.ToString(), Encoding.UTF8, "application/json");
                return response;
            }
            finally
            { db.Dispose(); }
        }

        public HttpResponseMessage CenterMasterAdd(Center pmm)
        {
            try
            {
                var re = db.BDL_CenterMasterInsUpd(pmm.CenterID.ToString(), pmm.CenterCode, pmm.CenterName, pmm.DateOfCreation, pmm.ActionD).FirstOrDefault();
                var response = Request.CreateResponse(HttpStatusCode.OK, re);
                string query3 = "{ \"Result \":\"Center Name Insert successfully\"}";
                var jObject = JObject.Parse(query3);
                response.Content = new StringContent(jObject.ToString(), Encoding.UTF8, "application/json");
                return response;
            }
            catch (Exception ex)
            {
                var response = Request.CreateResponse(HttpStatusCode.BadRequest, ex);
                return response;
            }
            finally
            { db.Dispose(); }
        }

        #endregion

        #region Area Master

        public HttpResponseMessage AreaMaster1Get(UserModel lc)
        {
            try
            {
                var re = db.BDL_Area1MasterRtr("All").ToList();
                var response = Request.CreateResponse(HttpStatusCode.OK, re);
                return response;
            }
            catch (Exception ex)
            {
                var response = Request.CreateResponse(HttpStatusCode.BadRequest, ex);
                string query3 = "{ \"Result \":\"Data Not Fetch\"}";
                var jObject = JObject.Parse(query3);
                response.Content = new StringContent(jObject.ToString(), Encoding.UTF8, "application/json");
                return response;
            }
            finally
            { db.Dispose(); }
        }

        public HttpResponseMessage AreaMaster1Add(AreaMaster1 pmm)
        {
            try
            {
                var re = db.BDL_Area1MasterInsUpd(pmm.AreaID.ToString(), pmm.CenterCode, pmm.AreaCode, pmm.AreaName, pmm.ActionD).FirstOrDefault();
                var response = Request.CreateResponse(HttpStatusCode.OK, re);
                string query3 = "{ \"Result \":\"Area Name Insert successfully\"}";
                var jObject = JObject.Parse(query3);
                response.Content = new StringContent(jObject.ToString(), Encoding.UTF8, "application/json");
                return response;
            }
            catch (Exception ex)
            {
                var response = Request.CreateResponse(HttpStatusCode.BadRequest, ex);
                return response;
            }
            finally
            { db.Dispose(); }
        }

        #endregion

        #region Society Master

        public HttpResponseMessage SocietyMaster1Get(UserModel lc)
        {
            try
            {
                var re = db.BDL_Society1MasterRtr("All").ToList();
                var response = Request.CreateResponse(HttpStatusCode.OK, re);
                return response;
            }
            catch (Exception ex)
            {
                var response = Request.CreateResponse(HttpStatusCode.BadRequest, ex);
                string query3 = "{ \"Result \":\"Data Not Fetch\"}";
                var jObject = JObject.Parse(query3);
                response.Content = new StringContent(jObject.ToString(), Encoding.UTF8, "application/json");
                return response;
            }
            finally
            { db.Dispose(); }
        }

        public HttpResponseMessage SocietyMaster1Add(SocietyMaster1 pmm)
        {
            try
            {
                var re = db.BDL_Society1MasterInsUpd(pmm.SocietyId.ToString(), pmm.CenterCode, pmm.AreaCode, pmm.SocietyCode,pmm.SocietyName,pmm.ActionD).FirstOrDefault();
                var response = Request.CreateResponse(HttpStatusCode.OK, re);
                string query3 = "{ \"Result \":\"Society Name Insert successfully\"}";
                var jObject = JObject.Parse(query3);
                response.Content = new StringContent(jObject.ToString(), Encoding.UTF8, "application/json");
                return response;
            }
            catch (Exception ex)
            {
                var response = Request.CreateResponse(HttpStatusCode.BadRequest, ex);
                return response;
            }
            finally
            { db.Dispose(); }
        }

        #endregion
    }
}

