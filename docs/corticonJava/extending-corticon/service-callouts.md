# Service Callouts

Service Callout (SCO) extensions are user-written functions that can be invoked in a Ruleflow.

In a Ruleflow, the flow of control moves from Rulesheet to Rulesheet, with all Rulesheets operating on a common pool of facts. This common pool of facts is retained in the rule execution engine's working memory for the duration of the transaction. Connection arrows on the diagram specify the flow of control. Each Rulesheet in the flow may update the fact pool.

When you add a Service Callout (SCO) to a Ruleflow diagram, you effectively instruct the system to transfer control to your extension class at a specific point in the flow. Your extension can directly update the fact pool, and your updated facts are available to subsequent Rulesheets.

[](/docs/assets/service_callout_ruleflow_diagram.png)

The rule flow uses two service callouts (Get Patient Info and then Get Procedure History), then uses the data in the Determine Approval Rulesheet, and finally passes control to Service Callout extension class Save Approvals.

Your Service Callouts use the Progress Corticon Extension API to retrieve and update facts. The package com.corticon.services.dataobject contains two Java interfaces:
Interface 	Purpose
com.corticon.services.dataobject.ICcDataObjectManager 	Provides access to the entire fact pool. Allows you to create, retrieve and remove entity instances.
com.corticon.services.dataobject.ICcDataObject 	Provides access to a single entity instance. Allows you to update the entity instance, including setting attributes and creating and removing associations.

Your Service Callout class must implement marker interface ICcServiceCalloutExtension.

Here is the source code for the service callout MedicalRecords.java: :


/* 
 * Copyright (c) 2016 by Progress Software Corporation. All rights reserved.
 */

package com.corticon.samples.extensions;

import java.util.ArrayList;
import java.util.Set;

import com.corticon.services.dataobject.ICcDataObject;
import com.corticon.services.dataobject.ICcDataObjectManager;
import com.corticon.services.extensions.Description;
import com.corticon.services.extensions.ICcServiceCalloutExtension;
import com.corticon.samples.simulation.*;

/**
 * This class provides sample Corticon service callouts. Callouts provide
 * a means to add custom features to Corticon for use in Corticon ruleflows.
 * Callouts are for integrating with external systems such as webservices. 
 * In a callout you can create and delete instances of Corticon entities,
 * set their properties and define associations. 
 * 
 * The samples in this class provide a simulation of retrieving patient 
 * medical data given a patient id. The class MedicalDataSimulator provides
 * a static set of patient and procedure data. In a real implementation 
 * this could be a class which gets data from a webservice, database, or
 * other source.
 * 
 */
public class MedicalRecords implements ICcServiceCalloutExtension {

	private static MedicalDataSimulator md = new MedicalDataSimulator();

	/**
	 * Service callout to retrieve patient descriptive information for
	 * the set of Corticon "Patient" entities. 
	 * 
	 * This callout demonstrates how to iterate over a set of Corticon
	 * entities and set attributes on them.
	 */
	@Description(lang = { "en" }, values = { "Service callout to retrieve patient descriptive information for the set of Corticon 'Patient' entities." })
	

Service Callout methods must be declared public static.

The system will recognize your Service Callout method if the method signature takes one parameter and that parameter is an instance of ICcDataObjectManager.


	public static void getPatientInfo(ICcDataObjectManager dataObjMgr) {
		// Get the set of "Patient" entities.
		Set<ICcDataObject> patients = dataObjMgr.getEntitiesByName("Patient");
		if (patients != null) {
			// Process each patient in the set.
			for (ICcDataObject patient : patients) {
				// Get the "id" attribute of the current patient.
				Long id = (Long) patient.getAttributeValue("id");
				
				if (id != null) {
					// Get the simulated information for this patient.
					PatientData pd = md.getPatientData(id.intValue());
					
					if (pd != null) {
						// Set patient information as entity attributes.
						patient.setAttributeValue("firstName",pd.getFirstName());
						patient.setAttributeValue("lastName", pd.getLastName());
					}
				}
			}
		}
	}

	/**
	 * Service callout to retrieve history of medical procedures for the
	 * set of Corticon "Patient" entities. 
	 * 
	 * This callout demonstrates how to create new Corticon entities and
	 * associate them with existing Corticon entities.
	 */
	@Description(lang = { "en" }, values = { "Service callout to retrieve history of medical procedures for the set of Corticon 'Patient' entities." })
	public static void getProcedureHistory(ICcDataObjectManager dataObjMgr) {
		// Get the set of "Patient" entities.
		Set<ICcDataObject> patients = dataObjMgr.getEntitiesByName("Patient");
		if (patients != null) {			
			// Process each patient in the set.
			for (ICcDataObject patient : patients) {
				// Get the "id" attribute of the current patient.
				Long id = (Long) patient.getAttributeValue("id");
				
				if (id != null) {
					// Get the simulated information for this patient.
					PatientData pd = md.getPatientData(id.intValue());
					
					// Get the medical procedure history for this patient.
					ArrayList<ProcedureData> td = pd.getProcedureRecords();
					
					// Add procedures to the patient entity
					for (ProcedureData r : td) {
						// Create a new "Procedure" entity.
						ICcDataObject p = dataObjMgr.createEntity("Procedure");
						
						// Set attributes on this entity.
						p.setAttributeValue("code", r.getCode());
						p.setAttributeValue("description", r.getDescription());
						p.setAttributeValue("date", r.getDate());
						
						// Associate it with the current patient.
						patient.addAssociation("procedure", p);
					}
				}
			}
		}
	}
	
	/**
	 * Service callout to save the approval state for each medical procedure
	 * for a set of Corticon "Patient" entities. 
	 * 
	 * This callout demonstrates how to iterate over a set of entities and
	 * associations to get the value of attributes. 
	 */
	@Description(lang = { "en" }, values = { "Service callout to save the approval state for each medical procedure for a set of Corticon 'Patient' entities." })
	public static void saveProcedureApproval(ICcDataObjectManager dataObjMgr) {
		// Get the set of "Patient" entities.
		Set<ICcDataObject> patients = dataObjMgr.getEntitiesByName("Patient");
		if (patients != null) {
			// Process each patient in the set.
			for (ICcDataObject patient : patients) {
				// Get the "id" attribute of the current patient.
				Long id = (Long) patient.getAttributeValue("id");
				
				// Process each "Procedure" association on the patient.
				Set<ICcDataObject> procedures = patient.getAssociations("procedure");
				for (ICcDataObject procedure: procedures) {
					
					// Get the value of the "approved" and "code" attributes on the procedure.
					Boolean approved = (Boolean) procedure.getAttributeValue("approved");
					String code = (String) procedure.getAttributeValue("code");
					
					// Update the procedure record.
					md.setProcedureApproval(id.intValue(), code, approved);
				}
			}
		}
	}

Recognized classes and methods are displayed in the Ruleflow Properties View/Service Name drop-down list when a Service Callout object is on a Ruleflow canvas:

The Service Callout API provides your extension class complete access to the fact pool, allowing you to:

    Find entities in several ways
    Read and update entity attributes
    Create and remove entity instances
    Create and remove associations

Refer to Service Callout Java sample project and the API Javadocs for more information.
